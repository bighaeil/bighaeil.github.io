---
title: "perspective - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:30:00
---

# perspective

하위 요소를 관찰하는 원근 거리를 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| 단위 | px, em, cm 등 단위로 지정 |  |

## ex)

관찰하고자 하는 요소의 상위요소에 perspective 속성을 적용해야 한다.
```css
.perspective {
  perspective: 500px; /* 원근감 */
}
.grand-parent {
  ...
  transform: rotateX(45deg);
  transform-style: perserve-3d;
  ...
}
.parent {
  ...
  transform: rotateX(45deg);
  transform-style: perserve-3d;
  ...
}
img {
  ...
  transform: rotate(45deg);
  ...
}
```

## perspective 속성과 함수의 차이점

`perspective` : 관찰 대상의 부모 요소에 적용 - 관찰하는 대상이 여러게일 경우
기준점은 *perspective-origin* 으로 설정

`transform: perspective()` : 관찰 하려는 대상에 적용
기준점은 *transform-origin* 으로 설정
