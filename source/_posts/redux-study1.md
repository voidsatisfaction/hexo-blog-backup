---
layout: post
title: React Native 공부기 ~ Redux 전편
categories:
  - JavaScript
  - React Native
tags:
  - JavaScript
  - React Native
  - Redux
---

## 나의 질문

 ``` js
  _showAddLectureRatingScreen() {
    const { lecture } = this.props;
    Actions.lectureRatingAdd({
      lecture,
    });
  }
```
여기서 lecture를 this.props에서 가져오는데 그 props는 어디에서 오는지가 궁금해

## 사부의 답변

props를 가져오는 곳이 3개가 있어요.

1. 부모 Component가 주는 경우
2. Redux가 주는 경우
3. react-native-router-flux 라이브러리를 사용하는데 그때 화면전환을 할때 Action 을 이용하는데 그 화면전환을 할때 주는경우

그렇다면 `const { lecture } = this.props;` 이건 어디서 가져왔을까요?

그걸 알려면 일단 얘가 screen 컴포넌트인지 자식 컴포넌트인지를 봅니다.

**왜냐면 자식컴포넌트는 무조건 부모 component에게만 props을 받고 redux나 router을 사용하지 않기로 했기 때문이죠**

### Component가 screen일 경우

부모 component가 없기때문에 redux나 router 입니다
근데 redux의 경우에는

``` js

LectureTimelineScreen과 redux

export default connect(
  (state) => ({
    user: state.userInfo,
  })
)(class LectureTimelineScreen extends Component {
  ...
}

```

보통 screen은 일반 자식 컴포넌트와 다르게 connect라는 걸로 component을 감싸는데 저 connect가 redux와 연결하는 고리 같은거에요.

저렇게 하면 component에서 this.props.user가 생겨요.
그리고 그 this.props.user는 현재 redux의 state의 userInfo가 들어가게 되는거죠
그래서 맨위를 보면 redux에서 받는 props을 알수 있어요

userInfo는 Reducer에 있는 userInfo.js 얘가 되는거구요

 ``` js

timeTableScreen과 redux

export default connect((state) => ({
  timeTable: state.timeTable,
  timeTableSetting: state.setting.timeTableSetting,
}))(class timeTableScreen extends Component {

```

timeTableScreen은 timeTable.js reducer와 setting.js reducer를 참조해서 가져오게 됩니다.

그렇다면 위에 redux에서 정의되지 않는 props는 router에 의해서 가져오는 props라고 생각할 수 있죠.

그렇다면 lectureDetail에서 가지고 있는 this.props.lecture는

 ```js

timeTableScreen의 _clickLecture함수

_clickLecture(time, day, lectureCode) {
    Actions.lectureDetail({
      time,
      day,
      lectureCode,
    });
}
```

timeTableScreen을 보면 저걸로 인해서 어디를 클릭했는지를 알수가 있어요.

월요일 1겐 이면 `day: 0 time: 0 `이 this.props 에 들어가게 되겠죠.

저렇게 해서 화면끼리 데이터를 교환할수 있어요.

```js
LectureDetail과 redux

export default connect(
  (state) => ({
    timeTable: state.timeTable,
  }),
  () => ({}),
  (stateProps, dispatchProps, ownProps) => ({
    ...dispatchProps,
    ...ownProps,
    lecture: stateProps.timeTable[ownProps.day][ownProps.time],
  })
)(class LectureDetailScreen extends Component {
```

일단 맨끝만 보면

`this.props.lecture`에 stateProps.timeTable[ownProps.day][ownProps.time],

가 들어간다는걸 알수가 있어요

lecture는 저기에서 오는거에요

그리고 this.props.timeTable 에는 state.timeTable 이 들어가겟죠

여기까지는 이해가 되시나요?

## 더 깊이 나아가서

**Q) 흠 철아 근데 redux의 state는 schema같이 형태만 정해져있는거야 아니면 정보가 저장되어있는거야?**

정보가 저장되어 있어요.
형태만 있는게 처음 상태에요

그리고 우리가 dispatch(action.xxxxxx) 이런식으로 쓰는 코드가 있잖아요.
그 action이 reducer 에 있는 안에 있는 코드를 불러내요.
그러면 그에 알맞게 state가 바뀌게 되는거죠.

가장 쉬운걸로는

 ``` js
 reducers/session.js

 export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    // focus action is dispatched when a new screen comes into focus
    case LOG_IN :
      return {
        ...state,
        sessionID: action.sessionID,
        logged: true,
      };

    case LOG_OUT :
      return {
        ...state,
        sessionID: '',
        logged: false,
      };

    default:
      return state;
  }
}

```

이렇게 되어 있잖아요

LoginScreen 보면 로그인 성공하면

`dispatch(action.login(sessionID));` 이런코드를 불러요

응응

저기 있는 login은

 ``` js
action/session.js

export const LOG_IN = 'LOG_IN';
export const LOG_OUT = 'LOG_OUT';

import { setSession } from '../api/base';

/*
 * 액션 생산자
 */

function login(sessionID) {
  setSession(sessionID);
  return { type: LOG_IN, sessionID };
}

function logout() {
  setSession('');
  return { type: LOG_OUT };
}
export default { login, logout };
```

여기 있는데

흐음 일단 setSession은 예외이니 그거 말고 login하면 return이

`return { type: LOG_IN, sessionID };`

이거죠


**Q) `dispatch(action.login(sessionID));`이 코드에서 session.js를 참조하라고 어디에 나와있어?**

action이 `import action from '../../actions'`

이런 코드 위에 있죠 그러면 action/index.js 을 참조하겟죠?

우리 컴포넌트들도 그냥 폴더까지만 참조하게하면 자동으로 index.js 을 참조하니까요

그래서 action/index.js을 보면 얘가 session을 참조해요

… 이게 참조표신가 보네

참조보다는 import가 맞겠죠.

그러면 `return { type: LOG_IN, sessionID };` 얘가 return 되고

그걸 dispatch가 reducer로 보내요.

그러면 또 reducer/index.js을 보고

지금 type: LOG_IN 이죠

`type: LOG_IN`

 ``` js
reducer/session.js

 export default function reducer(state = initialState, action = {}) {
  switch (action.type) {
    // focus action is dispatched when a new screen comes into focus
    case LOG_IN :
      return {
        ...state,
        sessionID: action.sessionID,
        logged: true,
      };

    case LOG_OUT :
      return {
        ...state,
        sessionID: '',
        logged: false,
      };

    default:
      return state;
  }
}
```

그러면 action.type이 LOG_IN이 코드가 실행이 되고

Q) 아 그럼 index.js안에 사실상 모든 reducer type가 들어가있는거나 마찬가진데 알기 쉽게 나눈거 뿐이구먼

저거 하나하나 import 하면 귀찮아 지니깐 바로 reducer 까지만 import 하도록 한거에요.

action도 마찬가지고요.

``` js

      return {
        ...state,
        sessionID: action.sessionID,
        logged: true,
      };
```

여기서 return값이

새로운 state.session 값으로 바뀌어요

 ``` js

const initialState = {
  sessionID: '',
  logged: false,
};

```

이게 초기치.

그래서 sessionID가 생기고 logged가 true가 되죠.

마찬가지로 reducer/schedule.js 을 보면

 ``` js
 reducer/schedule.js

 switch (action.type) {
    // focus action is dispatched when a new screen comes into focus
    case ADD_SCHEDULE :
      return [...state, action.newScheduleItem];

    case EDIT_SCHEDULE :
      return [
        ...state.slice(0, action.index),
        action.scheduleItem,
        ...state.slice(action.index + 1),
      ];
    case DELETE_SCHEDULE :
      return [
        ...state.slice(0, action.index),
        ...state.slice(action.index + 1),
      ];

    default:
      return state;
  }
```

스케쥴 추가면

뒤에 새로운 아이템을 붙이고

edit면 그 아이템만 교체

delete면 그거만 제거

---

아하 알겠어. 매우매우 알기 쉬운 설명이구만!

아 드디어 리덕스의 매커니즘을 이해했어 ㅠㅠ.

데이터변경을 위한 흐름을 파악하면 되는거네.

이런식으로 되어있다보니 아무래도 전에 봤던 그림이 어려워보였던 것 같아.

![Redux flow chart](http://image.slidesharecdn.com/reactreduxintroduction-151124165017-lva1-app6891/95/react-redux-introduction-33-638.jpg?cb=1448383914)

the upper picture is from http://www.slideshare.net/nikgraf/react-redux-introduction

이제는 이 그림도 이해할 수 있게 되었어!

리덕스의 매커니즘

dumbcomponent에서 데이터가변화 => screen으로 데이터가 감 => action생성 => dispather에 의한 redux상의 데이터변화(reducer)

2편에서 게속...
