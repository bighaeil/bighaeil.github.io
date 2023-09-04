---
title: "transform-origin - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:10:00
---

# transform-origin

요소 변환의 기준점을 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| x | left, right, center, %, 단위 | 50% |
| y | left, right, center, %, 단위 | 50% |
| z | 단위 | 0 |

## ex)

기본 중심축은 가운데
```css
img {
  ...
  transform: rotate(45deg);
  ...
}
```


이렇게하면 왼쪽 상단이 중심축
```css
img {
  ...
  transform: rotate(45deg);
  transform-origin: 0% 0%; /* 100% 100% 면 우측 하단이 기준점 */
  ...
}
```

