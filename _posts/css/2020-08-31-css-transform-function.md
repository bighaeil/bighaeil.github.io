---
title: "transform function - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-08-31T20:00:00
---

# transform 2D 변환 함수

| 값(변환함수) | 의미 | 단위 |
|:---|:---:|---:|
| translate(x, y) | 이동 (x, y) | 단위 |
| translateX(x) | 이동 (x) | 단위 |
| translateY(y) | 이동 (y) | 단위 |
|----
| scale(x, y) | 크기 (x, y) | 배수 |
| scaleX(x) | 이동 (x) | 배수 |
| scaleY(y) | 이동 (y) | 배수 |
|----
| rotate(degree) | 회전 (degree) | deg |
|----
| skew(x, y) | 기울임 (x, y) | deg |
| skewX(x) | 기울임 (x) | deg |
| skewY(y) | 기울임 (y) | deg |
|----
| matrix(n, n, n, n, n, n) | 2차원 변환 효과 (y) |  |

* 단위 : *px*, *cm*, *em* 등
* deg : 45도 를 표현하고 싶으면 *45deg*

## ex)

scale(1) 이면 - 1배

scale(0.8) 이면 - 0.8배

scale(1.5) 이면 - 1.5배

skewX(45deg) 이면 - X축으로 45도 비틈 - 음수 입력시 반대 방향

matrix : 잘 사용하지 않는다. 브라우저가 알아서 해줄 것임

```css
.box {
  ...
  transform: rotate(45deg);
  ...
}
```

동시 입력도 가능하다

```css
.box {
  ...
  transform: translate(10px, 20px) rotate(45deg);
  ...
}
```


## translate VS position

position : 배치를 하고 끝내는 개념
- 애니메이션에 특화 되어 있지 않음 (물론 애니메이션을 넣을 수 있지만)
- 부화가 많이 걸림
- 최적화되지 않음

translate : 상황에 때라서 실시간으로 변해야 된다면


```css
.box {
  ...
  transform: 1s;
  ...
}
.box:hover {
  ...
  transform: translate(30px, 30px);
  ...
}
```

---
---
# transform 3D 변환 함수

| 값(변환함수) | 의미 | 단위 |
|:---|:---:|---:|
| translate3d(x, y, z) | 이동 (x, y, z) | 단위 |
| translateZ(z) | 이동 (z) | 단위 |
|----
| scale3d(x, y, z) | 크기 (x, y,z) | 배수 |
| scaleZ(z) | 이동 (z) | 배수 |
|----
| rotate3d(x, y, z, a) | 회전 (x, y, z, 각도) | deg |
| rotateX(x) | 회전 (x) | deg |
| rotateY(y) | 회전 (y) | deg |
| rotateZ(z) | 회전 (z) | deg |
|----
| perspective(n) | 원근법(거리) | 단위 |
|----
| matrix3d(n, n, n, n, n, n, n, n, n, n, n, n, n, n, n, n) | 3차원 변환 효과 |  |

## ex)

3D 상테에서 30도 돌린다면
```css
.box {
  ...
  transform: rotateX(30deg);
  ...
}
```

멀리있는 이미지 영역과와 가까이 있는 이미지 영역과의 차이를 주고 싶다면 원근감을 사용
원근 거리를 넣고 싶을때
```css
.box {
  ...
  transform: perspective(100px) rotateX(30deg);
  /*transform: rotateX(30deg) perspective();*/
  ...
}
```

* perspective 는 가장 앞에 사용해야 한다.


