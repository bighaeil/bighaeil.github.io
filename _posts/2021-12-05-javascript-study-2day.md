---
title: "JAVASCRIPT STUDY FUNCTDION"
categories:
    - study
last_modified_at: 2021-12-08T12:35:00
toc: true
toc_sticky: true
---

# FUNCTDION

함수는 보통 무언가를 받아서 처리하고 결과를 반환하는 절차로 사용합니다.

하지만 javascript에서는 조금 더 특별합니다.

javascript funtion은 다른 모든 객체처럼 속성과 메서드를 가질 수 있는 `객체`입니다.

이를 염두하고 함수에 대해서 알아보자.


## 함수 표현식

```js
var f1 = function () {
}
function f2 () {
}
```

### 이름없는 함수 vs 이름있는 함수

함수 f1은 이름없는 함수를 선언하여 변수 f1에 할당한 형태입니다.

물론 아래처럼 선언할 수 있습니다.

```js
var f = function f1() {
}

f(); // possible
f1(); // error
```

이름있는 함수 f1을 선언하여 변수 f에 할당했지만 f1은 함수로 사용할 수 없습니다.

이름있는 함수는 __함수의 범위 안에서만 사용할 수 있습니다__. 여기서 f1은 변수안에 선언되어 범위가 한정된 것으로 보입니다. 그래서 에러를 발상하고 있습니다. 

결론적으로 개인적으로는 이름있는 함수는 되도록 사용하지 않습니다. 함수 범위가 모호해지기 때문에 뒤에서 알아볼 Hoisting 때문에라도 사용하지 않습니다. 





## 참조

> (function)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions]   
> (function guide)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Functions]   
