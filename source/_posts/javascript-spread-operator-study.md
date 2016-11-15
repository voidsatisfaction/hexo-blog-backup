---
layout: post
title: JavaScript Spread Operator
categories:
  - JavaScript
tags:
  - JavaScript
---

## 참조

- [전개 연산자 - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_operator)

- [Iteration protocols - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols)

## 용도

**Point**
1. 함수 호출 용 / 배열 리터럴 용 / 비구조화용
2. 더 나은 apply
3. 더 강력한 배열 리터럴



### 구문
```js
// 함수 호출 용
myFunction(...iterableObj);

// 배열 리터럴 용
[...iterableObj, 4, 5, 6];

// 비구조화(destructuring) 용
[a, b, ...iterableObj] = [1, 2, 3, 4, 5];
```

### 더 나은 apply
```js

function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction.apply(null, args);

// 이는 다음과 같다.

function myFunction(x, y, z) { }
var args = [0, 1, 2];
myFunction(...args);

// 이런 식의 사용도 가능하다.

function myFunction(v, w, x, y, z) { }
var args = [0, 1];
myFunction(-1, ...args, 2, ...[3]);

```

### 더 강력한 배열 리터럴
```js

var parts = ['shoulders', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes']; 
// ["head", "shoulders", "knees", "and", "toes"]

```

### new에 적용
```js

var dateFields = readDateFields(database);
var d = new Date(...dateFields);

```

### 더 나은 push
```js

var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// arr1에 arr2의 모든 항목을 덧붙임
Array.prototype.push.apply(arr1, arr2);

// 이는 다음과 같이 치환될 수 있음.
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);

```

### iterable에만 적용
```js

var obj = {"key1":"value1"};
function myFunction(x) {
    console.log(x); // undefined
}
myFunction(...obj);
var args = [...obj];
console.log(args, args.length) //[] 0

```

