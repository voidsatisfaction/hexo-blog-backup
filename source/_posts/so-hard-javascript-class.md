---
layout: post
title: 너무 헷갈리는 자바스크립트 Class개념
categories:
  - JavaScript
  - ECMA Script6
tags:
  - JavaScript
  - 객체지향
---

## 자료 출처
- [자바스크립트 클래스를 정의하는 3가지 방법](http://steadypost.net/post/lecture/id/13/)

- [자바스크립트 객체 생성](http://wit.nts-corp.com/2014/03/05/1042)

- [JavaScript 재입문하기 - MDN](https://developer.mozilla.org/ko/docs/A_re-introduction_to_JavaScript#.EC.82.AC.EC.9A.A9.EC.9E.90_.EC.A0.95.EC.9D.98_.EA.B0.9D.EC.B2.B4)

- [JavaScript Classes - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)

## 배경

리액트 네이티브를 쓰다가 보면, 자바스크립트 코어를 알아야 문제를 해결해야 하는 경우가 종종 발생한다.

그리고 꼭 리액트 네이티브에서 뿐 아니라 자주 사용하는 언어의 코어를 공부하는 것은 필수적이라고 할 수 있다.

애초에 내가 객체지향 프로그래밍에 대한 이해가 달려서 그런지 내용 자체가 지금은 아리송한 경우가 많은데, **객체 지향 프로그래밍**을 따로 공부해야 겠다.

## 핵심

- 자바스크립트에는 **클래스가 존재하지 않는다.** 클래스를 흉내낼 뿐이다.

## 의문

- 함수에서 객체를 생성하기 위한 `new` 라는 친구도 함수인가?