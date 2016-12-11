---
layout: post
title: High Order Component에 대하여
categories:
  - JavaScript
  - React Native
tags:
  - React Native
---

## 참조

- [recompose](https://github.com/acdlite/recompose)

## 배경

```js
// setFormState 

setFormState(name, value) {
  this.setState({
    [name]: value,
  });
}
```

위와 같은 `setFormState`가 smart컴포넌트를 변경하는 거의 모든 경우에서 중복되어서 사용되기 때문에

1. 재활용성을 높이고
2. render수를 줄이므로써 효율성을 높이고
3. 데이터 구조를 보다 명시적으로 나타내기 위해서

highOrderComponent를 새로 구성하기로 했다. 

## 핵심

```js
// from '../../_hocs/setFormState';

import React, { Component } from 'react';

interface config {
  (props: Object): configForms
}

interface configForms {
  forms: Object
}

export default setFormState = (config: config | configForms) => (BaseComponent: Comment) => (
   class extends Component {
     constructor(props) {
       super(props);
       this.setFormState = this.setFormState.bind(this);
       if (typeof config === 'function') {
         this.state = config(props).forms;
       } else if (typeof config === 'object') {
         this.state = config.forms;
       }
     }
     setFormState(name, value) {
       this.setState({
         [name]: value,
       });
     }
     render() {
       return <BaseComponent setFormState={this.setFormState} forms={this.state} {...this.props} />;
     }
  }
);

```

## 기본 내용

### interface

가장 먼저, interface와 관련된 내용이 나오는데 `interface`는 typeScript와 관련된 문법이다.(RN자체적으로 일부 typeScript문법을 지원해주는 것인지, 아니면 babel과 관련된것인지는 아직 확인 되지 않음)

[c.f) TypeScript](https://www.typescriptlang.org/docs/handbook/interfaces.html)

위의 `interface config` 이것은, config라는 데이터의 형태를 보기 좋게 정의한 것이다.

(처음 봤을때에는 c++에서 변수나 함수의 타입을 미리 정의하는것과 같다는 느낌이 들었다.)

즉, config라는 데이터는, 함수이며 인수로는 object를 받고 결과값은 configForms를 따른다는 것이다.

마찬가지로 configForms라는 데이터는, object이며, forms라는 속성을 갖고 그 속성의 값도 object라는 의미이다.

### setFormState

이 부분이 어려우니 차근차근 생각해야한다.

먼저 우리는 setFormState라는 함수를 export할 것인데 이 함수는 먼저

`config`라는 하나의 인자를 받고 이 인자는 앞서 interface에 정의한 `config`의 형태이거나 `configForms`의 형태이다.

이 함수는 함수를 리턴하는데(lamda) 리턴하는 함수는 인자로서 Comment형을 가진 BaseComponent라는 데이터이다.

이 함수는 하나의 이름이 없는 class를 리턴한다.

그 이름없는 class는 클로저 변수인 config의 type에 따라서 행위를 규정하고, setFormState를 bind하고

마지막으로는 `BaseComponent`에 setFormState, Forms, this.props(Redux등으로 받은 props)를 넘겨준다.

## 정리

이렇게 하면, setFormState의 중복을 해결할 수 있고

staticForm이라는 데이터를 setFormState함수의 인수에 추가하고 React Lifecycle인 `shouldComponentUpdate()`함수를 이용하여 render의 수를 줄일 수 있을것이다.

그리고 baseComponent에 사용되는 data를 타입과 함께 명시할 수 있는것도 크나큰 메리트이다.

> Special Thanks to JavaScript Goodparts 더글라스 크락포드 선생님!