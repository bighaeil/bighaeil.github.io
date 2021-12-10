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


## 화살표 함수(arrow funtion)

```js
const f1 = () => {
  return 1;
}
const f2 = () => 1; 
```

전통적인 함수표현의 간단한 표시입니다.

그렇다고 완전히 같은지는 않은 것 같습니다.

1. this나 super에 대한 바인딩이 없습니다.
2. new 키워드가 없습니다.
3. 스코프를 지정할 때 사용하는 메소드를 사용할 수 없습니다.
4. 생성자로 사용할 수 없습니다.
5. yield를 사용할 수 없습니다. (yield는 제너레이터 함수에서 사용하는 키워드 인데 기회가 되면 설명하겠습니다.)

화살표 함수의 특징은 간단한 표시이외에도 중요한 특징이 있습니다.

### 화살표 함수와 this

기존 function은 이 함수가 어디서 호출되는지에 따라 자신의 this를 정의했습니다.

```js
function Person() {
  this.age = 0;
  
  setInterval(function growUp() {
    this.age++; // this === window
  }, 1000);  
}
var p = new Person();
```

위 에서 Person은 age라는 멤버를 가지고 있어서 1초마다 증가시키려고 하지만 동작하지 않습니다. 이때 사용한 growUp 함수는 this를 전역 객체(여기서는 window)로 정의하고 있기 때문입니다. 즉 Person 안에서 growUp 함수를 선언한 것 처럼 보이지만 사실은 아닙니다.

여러가지 해결방법(바인딩)이 있겠지만 화살표 함수로 해결할 수 있겠습니다.

```js
function Person() {
  this.age = 0;
  
  setInterval(() => {
    this.age++; // this === Person의 인스턴스
  }, 1000);  
}
var p = new Person();
```





## 참조

> (function)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions]   
> (function guide)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Functions]   
> (arrow function)[https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions]   
> 
