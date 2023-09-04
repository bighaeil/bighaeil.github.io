---
title: "perspective-origin - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:40:00
---

# perspective-origin

하위 요소를 관찰하는 원근 거리를 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| x | left, right, center, %, 단위 | 50% |
| y | top, bottom, center, %, 단위 | 50% |

## ex)

perspective 속성이 부여된 조상 요소에 관찰 대상을 어디에서 볼 것 인가를 결정
```css
.perspective {
  perspective-origin: 50% 50%; /* 중심에서 관찰 */
}
.perspective {
  perspective-origin: 0 50%; /* 왼쪽에서 관찰 */
}
.perspective {
  perspective-origin: 50% 120%;  /* 아래쪽 영역 밖에서 관찰 */
}
```
