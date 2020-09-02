---
title: "animation - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-02T20:00:00
---

# animation

요소에 애니메이션을 설정/제어 - 단축 속성

애니메이션을 만들어주는 개념이 아닌 규칙에 설정된 규칙을 설정하는 개념

선언은 `@keyframes` 으로 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| animation-name | `@keyframes` 규칙의 이름을 지정 | none |
| animation-duration | 애니메이션의 지속 시간 설정 | 0s |
| animation-timing-function | 타이밍 함수 지정 [animation-timing-function](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function) | ease |
| animation-delay | 애니메이션의 대기 시간 설정 | 0s |
| animation-iteration-count | 애니메이션의 반복 횟수 설정 | 1 |
| animation-diraction | 애니메이션의 반복 방향 설정 | normal |
| animation-fill-mode | 애니메이션의 전후 상태(위치) 설정 | none |
| animation-play-state | 애니메이션의 재생과 정지 설정 | running |


## 표현
animation : 애니메이션이름 지속시간 [타이밍함수 대기시간 반복횟수 반복방향 전후상태 재생/정지]

## ex)

기본 중심축은 가운데
```css
.box {
  ...
  animation: hello 2s linear infinite both;
  ...
}

@keyframes hello {
  0% { width: 200px; }
  100% { width: 50px;}
}
```

hello 라는 `@keyframes` 으로 선언된 이름을 애니메이션으로 설정한다.

`%` 를 통해서 애니메이션을 정의 할 수 있다.
* `0%` 로 시작해서
* 중간 과정을 거쳐서
* `100%` 로 끝난다.

