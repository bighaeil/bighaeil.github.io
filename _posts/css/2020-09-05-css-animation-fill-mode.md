---
title: "animation-fill-mode - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-05T20:10:00
---

# animation-fill-mode

애니메이션의 전후 상태(위치)를 설정 - 개별 속성

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| none | 기존 위치에서 시작 -> 애니메이션 시작 위치로 이동 -> 기존 위치에서 끝 | 기본값 |
| forwards | 기존 위치에서 시작 -> 애니메이션 시작 위치로 이동 -> 애니메이션 끝 |  |
| backwords | 애니메이션 시작 위치로 이동 -> 기존 위치에서 끝 |  |
| both | 애니메이션 시작 위치로 이동 -> 애니메이션 끝 |  |

## ex)

기본은 요소 기본 상태에서 시작 (애니메이션 전 상태)  
2초 대기한 후에  
애니메이션 동작  
애니메이션이 끝나면 기존 위치로 다시 이동하는데  

both 설정을 적용하면  

애니메이션 시작 위치로 시작, 끝 위치로 끝난다.


```css
.box {
  ...
  animation: move 2s 2s;
  animation-fill-mode: both;
  ...
}

@keyframes move {
  0% {
    transform: translate(100px, 100px);
    background: blue;
  }
  100% {
    transform: translate(300px, 300px);
    background: yellow;
  }
}
```

