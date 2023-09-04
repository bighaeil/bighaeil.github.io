---
title: "animation-direction - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-05T20:00:00
---

# animation-direction

애니메이션의 반복 방향을 설정 - 개별 속성

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| normal | 정방향만 반복 | 기본값 |
| reverse | 역방향만 반복 |  |
| alternate | 정방향에서 역방향으로 반복(왕복) |  |
| alternate-reverse | 역방향에서 정방향으로 반복(왕복) |  |

## ex)

애니메이션이 반대 방향으로 동작한다.
```css
.box {
  ...
  animation: move 2s infinite;
  animation-direction: reverse;
  ...
}

@keyframes move {
  0% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(100px, 0);
  }
  100% {
    transform: translate(0, 0);
  }
}
```
* animation-iteration-count 와 animation-direction 의 alternate 을 같이 사용하면 정상적으로 동작하지 않을 수 있다.
* 정방향으로 한번돌고 역방향으로 한번도는 것은 동작을 한번더 하는 것과 같기 때문이다.
* 즉 alternate-count 를 한번더 소비하는 것과 같다.
