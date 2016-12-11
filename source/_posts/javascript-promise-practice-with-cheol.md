---
layout: post
title: 사부와 함께하는 Promise 이해하기
categories:
  - JavaScript
  - ECMA Script6
tags:
  - JavaScript
---

## 배경

Nodejs 비동기 프로그래밍 환경에서 정말 중요한 Promise가 헷갈려서 사부에게 도움을 청했다.

그래서 다음과 같은 코드를 받았다. 그리고 그 밑은 나의 해석.

## 핵심

- Nodejs는 모든 scope에서 비동기적인 io 매커니즘을 가지고 있다.

- Promise는 그 자체가 객체로서, resolve() 나 reject() 를 호출하게 하므로서, 함수 내의 모든 실행이 해결된 것을 나타낸다.

- 따라서, Promise객체의 return으로 동기적인 함수 실행을 이어나갈 수 있다.(콜백함수 효과)

- Promise객체의 return이 없다면 뒤에 붙는 then자체는 사실상 의미가 없다.

NodeJS의 비동기 처리

tick이 달라지는 계기를 주는 이벤트가 생기면 그래야지 그것이 event loop에 들어가게 되고 나머지 같은 틱에 있는 처리들은 동기적으로 한다
그리고 같은 틱의 처리가 끝나면 event loop에 있는 것들도 마찬가지로 한다.

같은 틱에서는 동기적으로 프로그램이 동작하고
틱과 틱 사이에서도 동기적으로 프로그램이 동작한다.

**one-tick에 같이 실행됨 -> 동기**
**one-tick에 실행이 안되고, event에 의해서 다른 tick에서 실행이 됨 -> 비동기**

```js
function wow (text, cb) {
    cb(text+ 'wow')
    console.log('hi world!')
  }
  wow('abc', (wowText) => console.log(wowText))
  console.log(1)
```

이 예에서는 콜백이어도 같은 틱에서 처리하니까 콜백을 먼저함 동기적으로

## Promise 기본 내용

- [promise_test1.js - g6ling](https://gist.github.com/g6ling/bbc08b8f217d50e72e4873dab056ed3f)

- [promise_test2.js - g6ling](https://gist.github.com/g6ling/ecf2a15cd1afa8ab10047274bc4c914d)

- [promise_test3.js - g6ling](https://gist.github.com/g6ling/0c312b7cfb50a70d83d01bf9b7e4c025)

- [promise_test4.js - g6ling](https://gist.github.com/g6ling/96980fb868f4aacee554d9eb7a642532)

- [Promise 실행순서 이해하기 - g6ling](https://g6ling.github.io/2016/11/18/dive-into-promise-chain/)

- [Promise - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)

- [Promise.prototype.then() - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then#Chaining)

## 참고 내용

- [Callbacks, Promises, and Coroutines](http://www.slideshare.net/domenicdenicola/callbacks-promises-and-coroutines-oh-my-the-evolution-of-asynchronicity-in-javascript)
  - p.s 이 슬라이드는 35,36에 오류가 있다. 그 내용은 댓글에서 확인.

- [Node.js - Definitive Design Definition - Tutorial Series #0](https://www.somenathghosh.space/2016/03/20/node-js-definitive-design-definition-tutorial-0/)


## 발전

```js

var f1 = function () {    
   setTimeout(function(){
      console.log("f1", "First function call...");
   }, 0);
};

var f2 = function () {
    console.log("f2", "Second call...");
};

f1(); f2();

// f2 Second call...
// f1 First function call...

// 일단 위의 프로그램이 실행되면
// first-tick일때(즉, 호출하자마자)f1, f2가 각각실행된다.(같은 tick에서는 동기)
// 근데 f1에서는 setTimeout이라는 함수가 있으므로 event loop위에 올려놓는다.
// 하지만 f2는 console.log만 존재하므로 그것을 실행한다.

// second-tick일때는 0초뒤의 경우(setTimeout에서 0이 지정되었으므로)이므로 
// event loop위에 올려놓았던 setTimeout의 내용을 실행한다.
// 그것은 console.log()이므로
// 그대로 출력한다.

```