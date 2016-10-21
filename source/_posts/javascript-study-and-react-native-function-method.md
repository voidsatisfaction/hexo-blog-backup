---
layout: post
title: React Native의 원리 및 JavaScript의 함수
categories:
  - JavaScript
  - React Native
tags:
  - JavaScript
  - React Native
---

## 출처 및 들어가 보면 좋은 사이트
- 사부의 말

- [Intoriduction to JavaScript - Mozilla 재단](https://developer.mozilla.org/ko/docs/A_re-introduction_to_JavaScript)

- [객체지향 자바스크립트의 소개 - Mozilla 재단](https://developer.mozilla.org/ko/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)

## 의문

내가 React Native코드를 작성하는 과정에서 다음과 같은 일이 있었다.

ListView의 renderRow함수를 this.renderRow로 하고
그 안의 TouchableOpacity의 onPress속성에 부모 컴포넌트에서 받아온 함수를 넘겨주려고 했는데,
막상 클릭해보니 `this.props.함수 == undefined` 이라는 것이었다.

즉, this.props에는 그 함수가 존재하지 않는다는 것이었는데, 나는 renderRow라는 함수를 component class안에 정의해두었기 때문에
당연히 this가 그 component를 가리킨다고 생각했다.

```js

export default class SchoolBoardList extends Component {
  static propTypes = {
    boardItems: PropTypes.array.isRequired,
    boardItemOnpress: PropTypes.func.isRequired,
  }
  constructor(props) {
    super(props);
    const ds = new ListView.DataSource({ rowHasChanged: (r1, r2) => r1 !== r2 });
    this.state = {
      dataSource: ds.cloneWithRows(this.props.boardItems),
    };
    this.renderRow = this.renderRow.bind(this);
  }

  renderRow(rowData) {
    const { title, date, content, author, good, chat } = rowData;
    return (
      <TouchableOpacity
        style={style.item}
        onPress={() => { this.props.boardItemOnpress(); }}
      >
        ...
      </TouchableOpacity>
    );
  }

  render() {
    const { dataSource } = this.state;
    return (
      <View style={style.container}>
        <ListView
          dataSource={dataSource}
          renderRow={this.renderRow}
          automaticallyAdjustContentInsets={false}
        />
      </View>
    );
  }
}
```

이런식으로 되어있는 코드였다.

그래서 어? 어쩐일이지? 하면서 TouchableOpacity내부의 onPress속성 안에 console.log(this)를 넣어보니 웬걸 this는 전역객체를 의미하고 있었다!

그래서 나는 "뭐지? 난 클래스 안에다가 함수를 정의했는데? 왜 this가 전역객체인거야!" 하고 대혼란에 빠졌다.

## 사부의 답변

그래서 나는 바로 사부에게 물어보았다. "왜 클래스 안에다가 함수를 정의했는데 this가 전역이 되는가?" 라고.

그래서 사부는 나에게 "React Native에서 render를 누가 부를까요? 라고 되물었다."

답은 'React Native 엔진'이었다.

사부에 의하면 React Native엔진의 행동은 다음과 같다.(다소 차이점이 있다고는 하지만 지금은 이렇게 알아둬도 된다고 했다.)

---

**RN 엔진의 행동**

1. index.js 실행

2. React Native Lifecycle실행

3. index.js안의 new component를 만듬

4. component.render()를 실행해서 view를 만듬

5. 동작

**메소드와 함수**

> 클래스.함수 로 실행시키면 클래스 안에 있는 함수를 실행시키는 거여서 메서드 로 처리해요.  

> 근데 형은 보통 this.함수를 클래스 안에서 사용하잖아요 이 경우에는 React Native입장에서 this.함수의 결과가 함수잖아요 그래서 함수로 실행시켜요.

---

즉 React Native엔진이 component.render()를 실행할때는 this가 component가 되니까 즉 class 가 되니까 

render()함수 내에서 사용한 this.함수명 = 메소드(component 클래스 안에서의 함수 ex: 위의 경우 `renderRow()`와 같은 함수) 이렇게 되는거고
  
근데 버튼을 클릭하는 행동 같은 경우에는 class안에서 this를 정의해버렸으니 그 this가 전역객체니까 그걸 다시 component로 바꾸기 위해서 constructor나 render안에서 bind(this)하는 것이었다.

즉 그냥 renderRow함수 내에서 `<TouchableOpacity onPress={this.props.boardItemOnpress}` 이렇게만 하면 RN엔진이 **component.renderRow이렇게 실행하지 않기**때문에 renderRow안의 this는 전역 객체가 되어 버리고

전역 this에는 this.props.boardItemOnpress가 존재하지 않으니까 `this.props.함수 == undefined` 이렇게 되었던 것이었다.

그렇기 때문에 이 문제를 해결하기 위해서는 클래스 내부의 constructor함수에서 `this.renderRow = this.renderRow.bind(this)` 이렇게 this의 지정을 component class로 명확히 해줘야 한다.

이는 `함수.bind(this)`를 해주기 전까지는 **어디에서 혹은 무엇이** 그 함수를 부르는가가 중요하지만, `함수.bind(this)`를 해주는 행위는 **어디에서 그 함수를 호출하든 함수 내부의 this를 지정** 해주는 것이다.

## 느낀 점

어떠한 기술을 확실히 '내 것'으로 만들기 위해서는 그 기술의 core를 이해하지 않으면 안된다.

이번 일을 계기로 JavaScript의 class개념, 함수 / 메소드 개념 React Native의 Lifecycle같은 개념을 알아야 하는 것의 중요함을 깨닫게 되었다.

자바스크립트에 대해서 깊이 이해하고 싶은 분들은 앞에서 소개한 mozilla재단의 javascript관련 문서를 읽는 것을 추천합니다.

역시 프로그래밍은 재미있다! 그리고 사부는 최고다.

