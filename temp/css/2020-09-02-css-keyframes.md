---
title: "@keyframes - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-02T20:10:00
---

# @keyframes

2개 이상의 애니메이션 중간 상태(프레임)을 지정

이 프레임은 애니메이션 속성으로 제어할 수 있다.

## ex)

```css
@keyframes 애니메이션이름 {
  0% { 속성: 값; }
  50% { 속성: 값; }
  100% { 속성: 값; }
}
```

*backface-visibility: hidden;* 뒷면이 나오는 시점에서 요소가 나오지 않음

