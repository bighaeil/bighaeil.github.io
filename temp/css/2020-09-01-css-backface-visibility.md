---
title: "backface-visibility - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:50:00
---

# backface-visibility

3D 변환으로 회전된 요소의 뒷면 숨김을 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| visible | 뒷면 숨기지 않음 (반전됨) | 기본값 |
| hidden | 뒷면 숨김 |  |

## ex)

```css
img {
  ...
  transform: rotateY(180deg); /* 요소 뒤집음 - 이미지 반전 */
  backface-visibility: hidden;
  ...
}
```

*backface-visibility: hidden;* 뒷면이 나오는 시점에서 요소가 나오지 않음

