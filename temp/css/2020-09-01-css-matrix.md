---
title: "matrix() - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-01T20:50:00
---

# matrix(a, b, c, d, e, f)

요소의 2차원 변환(Transforms) 효과를 지정

scale(), skew(), translate(), rotate() 까지 지정한다.

> 요소에 일반 변환(Transforms) 함수(2D, 3D)를 사용하더라도 (즉 scale 이나 skew 같은 함수를) 브라우저에 의해 matrix 함수로 계산되어 적용됨(자동으로 변환대어 들어감)
> 즉 굳이 어려운 matrix 를 사용하지않고 직관적인 **일반 변환 함수**를 사용하면 된다.


## ex)

matrix(a, b, c, d, e, f) 는

3 X 3 행렬
|  |  |  |
|:---:|:---:|:---:|
| a | c | e |
| b | d | f |
| 0 | 0 | 1 |

같이 들어간다.

* 보기만해도 머리아프다. 그냥 일반 변환 함수를 사용하자.
