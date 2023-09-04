---
title: "animation-play-state - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-05T20:20:00
---

# animation-play-state

애니메이션의 재생과 정지를 설정 - 개별 속성

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| running | 애니메이션을 동작 | 기본값 |
| paused | 애니메이션 동작을 정지 |  |

## ex)


```css
.box {
  ...
  animation: size-up 3s linear infinite alternate;
  ...
}
.box:hover {
  ...
  animation-play-state: paused;
  ...
}

@keyframes size-up {
  0% {
    width: 100px;
  }
  100% {
    width: 100%;
  }
}
```
