---
layout: post
title: React Native 공부기 ~ Redux 후편
categories:
  - JavaScript
  - React Native
tags:
  - JavaScript
  - React Native
  - Redux
---

## 지난번에 공부한 것들

- props의 공급원

- dispatch(action.login(sessionID))의 의미

- Redux의 매커니즘

## 다시 이야기로 돌아와서

![redux](https://css-tricks.com/wp-content/uploads/2016/03/redux-article-3-03.svg)

저런식으로 redux에 state을 저장해서 다른 컴포넌트들이 그걸 참조하는거에요.

**Q) 그럼 dumbcomponent에서 데이터가변화 => screen으로 데이터가 감 => action생성 => dispather에 의한 redux상의 데이터변화(reducer)** 요로코롬 이해하면 될까?

네.

아 이제 완벽히 이해된다.

connect가 뭔지도 아시겟죠?

다른 일반적인 react-redux아키텍쳐랑 조금 달라서 아마 어려울수도 있었을거에요.

- dumbcomponent에서 데이터가변화 => screen으로 데이터가 감 => action생성 => dispather에 의한 redux상의 데이터변화(reducer)

이게 아니라,

- dumbcomponent에서 데이터가변화 => action생성 => dispather에 의한 redux상의 데이터변화(reducer)

이거여서.

보통은 react의 state을 아에 쓰지 않거든요.

web front 의 경우에는 그냥 전부다 redux로 처리하니까 textInput 같은것도 redux state를 바꾸는걸로 해요.

근데 저희는 redux state을 핸드폰에다가 저장을 해놔서

그렇게 자잘한걸 전부다 redux로 처리를 하면 퍼포먼스가 나빠질 것 같아서, 적절히 나눈거구요.

대충 redux 에 대해 이해가 되셧나요?

---

**Q) redux로 처리하는것과 react자체 state로 처리하는 것의 차이는 뭐야?**

- redux로 처리는 action, dispatch을 이용해서 redux의 state를 바꿔서 view을 바꾸는 거구요.

- react 자체 state는 this.setState을 통해서 view를 바꾸는 거죠.

그리고 사실 redux로 처리를 하면 `action -> middleware -> reducer`의 형태로 redux state가 변경되는데, 이 과정에서 여러가지를 할수가 있어요

반면에 setState는 setState 만으로 값을 바꾸는 거여서 복잡한 처리에는 좋지 않아요.

그렇지 middleware에서 데이터를 가공하든 다른곳에 통신을 하던 할 수 있으니까 redux는

**Q) 근데 내 짧은 생각으로는 아무래도 redux가 여러가지 모듈을 거치니까 더 느릴거 같다는 생각이드는데..**

redux가 더 느릴걸요.

더 느린데 할수있는게 많은거죠.

자유도 라고 해야하나요.

일단은 액션만 생성하면 redux의 정보를 변경할 수 있어요.

## this.props.lecture는 어디에서 오는가?

아 그 props 가 어디서 오는지 설명해 드릴게요.

``` js
screen/LectureDetailScreen

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

this.props.timeTable에 state.timeTable을 연결시켜요

또한, connect의 3번째 인수는

``` js

(stateProps, dispatchProps, ownProps) => ({
   ...dispatchProps,
   ...ownProps,
   lecture: stateProps.timeTable[ownProps.day][ownProps.time],
 })

```

이런 함수인데

여기서 state.Props는 저기 위에 있는 `{ timeTable: state.timeTable }`가 들어가 있어요.

그리고 ownProps는 원래 얘가 가지고 있는 props을 의미해요.

lectureDetail은 timeTableScreen 에서 오는 얘인데

그때 `Action.lectureDetail({ day, time})`으로 보냈으니 `this.props.day, this.props.time` 을 받게 되죠

ownProps.day과 ownProps.time 은 timeTable에서 받은 day와 time 이에요

우리가 lectureDetail에서 필요한건 timeTable이 아니라 특정 timeTable안에 있는 특정 lecture 이기 때문에,

**`lecture: stateProps.timeTable[ownProps.day][ownProps.time],` 이걸 써서 this.props.lecture에 lecture을 주는거에요.**

그래서 우리는 컴포넌트 안에서 this.props.lecture 만으로 얘의 lecture을 알수가 있죠.

사실 그냥 `this.props.lecture = this.props.timeTable[this.props.day][this.props.time]` 와 같이 해도 되는데

저건 별로 좋지도 않고

**데이터 가공이랑 데이터 사용을 분리해서 적어놔야 보기가 편해요.**

"아 이 컴포넌트는 lecture을 쓰는구나 timeTable 전체를 안쓰는군." 이렇게요.


``` js
screen/scheduleScreen

export default connect((state) => {
  const timetableScheduleItems = state.timeTable ? state.timeTable.reduce((sum, dayTimetable) => {
    const dayTimetableSchedules = dayTimetable.reduce((daySum, lecture) => {
      const timelines = lecture.timelines.map((timeline) => ({
        ...timeline.info,
        lectureName: lecture.lectureDPName,
      }));
      return [...daySum, ...timelines];
    }, []);
    return [...sum, ...dayTimetableSchedules];
  }, []) : [];
  const scheduleItems = [
    ...timetableScheduleItems,
    ...state.schedules,
  ];
  return ({
    scheduleItems,
  });
})(class ScheduleScreen extends Component {
```

이건 scheduleScreen 인데 얘도 timeTable을 가공해서 shceduleItem을 만드는거에요.
