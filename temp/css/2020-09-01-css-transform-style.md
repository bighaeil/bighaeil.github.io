---
title: "transform-style - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:20:00
---

# transform-style

3D 변환 요소의 자식 요소도 3D 변환을 사용할지 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| flat | 자식 요소의 3D 변환을 사용하지 않음 | flat |
| preserve-3d | 자식 요소의 3D 변환을 사용함 |  |

## ex)

부모와 자식 요소가 아래와 같이 있을 때
```html
<div class="perspective">
  <div class="grand-parent">
    <div class="parent">
      <img />
    </div>
  </div>
</div>
```

transform-style 의 기본값은 flat으로 자식의 요소에 3D 변환이 적용되지 않는다.
```css
.perspective {
  perspective: 500px; /* 원근감 */
}
.grand-parent {
  ...
  transform: rotateX(45deg);
  ...
}
.parent {
  ...
  transform: rotateX(45deg);
  ...
}
img {
  ...
  transform: rotate(45deg);
  ...
}
```

보모의 속성에 3D 적용을 하겠다는 선언을 하여 (perserve-3d) 자식의 요소에 3D 효과가 적용된다.
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
* 자식의 자식 요소도 3D 변환을 적용하고 싶으면 보모에 *perserve-3d* 를 적용해야 한다.

