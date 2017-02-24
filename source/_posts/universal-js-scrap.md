---
layout: post
title: Universal JavaScript 스크랩
categories:
  - JavaScript
tags:
  - JavaScript
---

## 참조

- [Universal JavaScript](https://medium.com/@mjackson/universal-javascript-4761051b7ae9#.faxzeds0v)

## 기본 내용

### Universal JavaScript

In the beginning, there was Netscape. And Netscape wanted to run Scheme in Netscape Navigator. So they hired Brendan Eich to work on it. But then they changed their minds and decided they wanted Java instead. And lo, JavaScript was born. And it was good (enough).

Some years later, Ryan Dahl had this crazy idea to pair Google’s V8 JavaScript runtime with libev so developers would have a way to run their JavaScript outside the browser. And node.js became a thing. And npm. And the people rejoiced.

And people started writing web servers in JavaScript, and flying helicopters with JavaScript, and putting it on tablets and mobile phones, and embedding it in thermostats and refrigerators and pretty much anywhere they pleased. And there was a proliferation of JavaScript. And Serious Developers™
despised the common people who wrote JavaScript, but the people just kept writing more and more JavaScript.

And the people sought for a word to describe this widespread adoption of JavaScript, because the term “JavaScript” on its own was not sufficient to describe its vastness. So Charlie Robbins suggested that the term “Isomorphic JavaScript” might be used to describe JavaScript code that “can execute both on the client and the server”. And nobody knew what the hell it meant, but now instead of just writing JavaScript the people were writing Isomorphic JavaScript.

Wait … huh?

When coining the term Isomorphic JavaScript, Robbins explains that he meant “that any given line of code (with notable exceptions) can execute both on the client and the server”. However, if we examine more closely the meaning of the word isomorphic we read “corresponding or similar in form and relations”. In other words, two entities that are not the same but only look the same. This would be a great word to use when describing the relationship between jQuery and Zepto or Underscore and lodash, for example. These libraries are similar in form (they share the same API) but differ in underlying ideas and philosophy.

Instead, what we need is a word that describes the same code but running in a different environment. Nowadays we run JavaScript code not only on servers and in browsers, but on mobile and embedded devices as well. We’re running it on Raspberry Pis and Wii Us and iPhones. But this is a purely technical argument. What’s even more important is conveying understanding.

But of course, understanding is highly subjective. Recently, Ryan Florence and I began conducting React.js Training courses full-time. Up to this point we have trained several hundred developers, and it’s not uncommon for someone to ask what the word isomorphic means. Now, this is purely anecdotal evidence, but when we use the word universal instead of isomorphic everyone gets it. It may have something to do with Apple using that same word to describe application bundles that ran on both architectures back when they made the switch from PowerPC to Intel.

It’s true that there are two hard problems in computer science and one of them is naming things. Why? Because good names are important. A good name teaches about purpose and responsibility, so you have to spend some time thinking about it.

So let’s give our JavaScript code a name that people can understand; a name that indicates what it actually does instead of introducing words into the common vernacular that clearly don’t belong there; a name that teaches people that it runs not only on servers and browsers, but on native devices and embedded architectures as well.

Let’s call it Universal JavaScript.

My thanks to Ryan Florence, Pete Hunt, Peter Cooper, Dan Abramov, and Mark Dalgleish for reviewing this post prior to publication. Also, thanks to Ryan for riffing on these ideas with me.

## 정리

자바스크립트는 웹 환경에서 클라이언트에 작동하기 위한 스크립트 언어로 출발하였으나 지금은 위의 글에도 나와있듯이 서버 환경, iphone등 그 영역을 점차 확장시켜 나가고 있다.

초기 자바스크립트의 경우 넷스케이프가 Scheme을 도입하려 했다는게 정말 충격적이었다.(그래서 함수 기반이구나..!)

내가 스킴을 공부했던게 이렇게 이어질 줄이야.

정말 인생이란 알 수 없는것 같고, 스티브 잡스의 Connecting the dots가 와닿게 만든 글이다.