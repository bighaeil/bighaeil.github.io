---
title: "variable,constant - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-06T20:50:00
---


# variable

어떤 값을 어딘가(메모리)에 보관할때 사용

이 어딘가의 값이 변할 수 있거나 계속 변하는 경우에 사용

같은 블록에 같은 이름으로 쓸 수 없음

ex)
```js
var num = 10;
let value = 20; // ES6
```

> ES5 이전 구형 브라우저 같은 경우는 변수로 `var`를 사용한다.  
> var 는 같은 블록에 같은 이름으로 쓸 수 있지만 오류가 생길 요소가 다분하다.  
> 구형 브라우저에서는 아직도 사용하지만 되도록 사용하지 말아야 한다.


# constant

변하지 않는 수 - 상수

한번 정의하면 바꿀 수 없다.

nameing 은 항상 대문자를 사용하고 띄어쓰기에 언더바(_)를 사용 한다.

ex)
```js
const MY_NAME = "NAME";
```

> ECMA 6 부터는 let, const 도 존재하지만


