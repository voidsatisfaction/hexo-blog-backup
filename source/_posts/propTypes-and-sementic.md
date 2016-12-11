---
layout: post
title: PropTypes과 Semantic Commit Messages 
categories:
  - JavaScript
  - React Native
tags:
  - JavaScript
  - GitHub
---

## 참조

- [React.jsのProp](http://qiita.com/koba04/items/bc13d1f42964278ae14e)
- [KARMA Git Commit Msg](http://karma-runner.github.io/1.0/dev/git-commit-msg.html)
- [Semantic Commit Message](https://seesparkbox.com/foundry/semantic_commit_messages)

## 배경

사부의 커밋 메세지를 보면 feat:, fix: 이런 것들이 붙어져 있어서 그것에 대한 유래를 물어보았다.

그리고 전부터 대충은 알고 있던 React Native의 PropTypes에 대해서 한 번은 정리할 필요가 있을 것 같아서 포스팅을 하게 되었다.

## 핵심

### Semantic Commit Message Examples

1. chore: add Oyster build script (oyster build가 뭐죠? 아시는 분 알려주세요!) 
2. docs: explain hat wobble
3. feat: add beta sequence
4. fix: remove broken confirmation Message
5. refactor: share logic between a and b
6. style: convert tabs to spaces ... (and so on)
7. test: ensure Tayne retains clothing

### PropTypes

PropTypes는 Component의 외부로부터 받아온 prop을 validation하기 위해서 prop의 type을 명시적으로 제한한다.

```js

React.PropTypes.array           // 配列
React.PropTypes.bool.isRequired // Booleanで必須
React.PropTypes.func            // 関数
React.PropTypes.number          // 数値
React.PropTypes.object          // オブジェクト
React.PropTypes.string          // 文字列
React.PropTypes.node            // Renderできるもの
React.PropTypes.element         // React Element
React.PropTypes.instanceOf(XXX) // XXXのinstanceかどうか
React.PropTypes.oneOf(['foo', 'bar']) // fooかbar
React.PropTypes.oneOfType([React.PropTypes.string, React.PropTypes.array]) // 文字列か配列
React.PropTypes.arrayOf(React.PropTypes.string)  // 文字列の配列かどうか
React.PropTypes.objectOf(React.PropTypes.string) // 文字列の値を持っているか
React.PropTypes.shape({                          // 指定された形式を満たしているかどうか
  color: React.PropTypes.string,
  fontSize: React.PropTypes.number
});
React.PropTypes.any.isRequired  // なんでもいいけど必須

// カスタムの制約も定義出来る(ダメな場合はError投げる)
customPropType: function(props, propName, componentName) {
  if (!/^[0-9]/.test(props[propName])) {
    return new Error('Validation failed!');
  }
}

```

위와 같은 종류의 PropTypes를 이용할 수 있다.

## 정리

> 프로그래밍의 세계에서는 알기 쉬운게 최고다! 나를 배려하고 나와 협업하는 동료를 배려하자.