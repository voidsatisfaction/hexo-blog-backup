---
layout: post
title: React Native with 최신 자바스크립트 문법
categories:
  - JavaScript
  - React Native
tags:
  - JavaScript
  - React Native
---

## 참조

- [JavaScript Environment - React Native](http://facebook.github.io/react-native/docs/javascript-environment.html)

- [babeljs.io](http://babeljs.io/)

- [Flowtype.org](https://flowtype.org/)

- [Object Spread](https://github.com/sebmarkbage/ecmascript-rest-spread)

- [esnext](https://github.com/esnext/esnext)

## 고찰 

**사부가 쓰던 모든 최신문법이 여기 있었다.**

또한 React Native는 iOS simulator에서는 **JavaScriptCore(Safari의 자바스크립트 엔진)**를 사용하고,

Chrome debugging에서는 V8엔진으로 따로 사용한다는 것을 알게 되었다.

## 여담 및 재미있는 코드

[object.assign() - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

```js
function test() {
  let a = { b: {c:4} , d: { e: {f:1}} }
  let g = Object.assign({},a)
  let h = JSON.parse(JSON.stringify(a));
  console.log(g.d) // { e: { f: 1 } }
  g.d.e = 32
  console.log('g.d.e set to 32.') // g.d.e set to 32.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: { f: 1 } } }
  h.d.e = 54
  console.log('h.d.e set to 54.') // h.d.e set to 54.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: 54 } }
}
test();
```

