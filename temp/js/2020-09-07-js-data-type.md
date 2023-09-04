---
title: "data type - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-07T20:00:00
toc: true
toc_sticky: true
---

# data type - call) 자료형

[Data Type](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)

```js
var something;
```

변수를 선언만하면 위가 어떤 타입인지 알 수 없다.

```js
var something = 'string';

somthing = 123;
somthing = true;
```

변수에 문자열을 입력하면 타입은 `string`이 된다.

string 타입의 변수에 숫자를 넣으면 `number` 타입

true, false 를 넣으면 `boolean` 타입이 된다.

이를 `동적(dynamic) 타입` 이라고 한다.


## 타입 종류

* 기본 타입(Primitive values)
  * boolean
  * null
  * undefined
  * number
  * string
  * symbol(ECMAScript 6 에 추가됨)
* 객체(objects)


## 기본 타입


### boolean

true : 참

false : 거짓


### null & undefined

null : 값이 없다.

```js
typeof null; // 'object'
```

즉 아무 값이 없다는 object 이다.

undefined : 비여있다.

```js
typeof undefined; // 'undefined'
```

즉 비어있다는 의미


### number

123 : 정수는 숫자

96.21 : 실수도 숫자

NaN : 숫자형이긴 하지만 숫자가 아닌 값 (Not a Number)

```js
var realNumber = Number('10'); // 10
var notNumber = Number('Ten'); // NaN
```

문자열 10은 숫자로 `형변환` 했을때 10이라는 숫자로 표현할 수 있기 때문에 숫자가 가능하지만
문자열 Ten은 숫자로 표현할 수 없기 때문에 `NaN` 이라는 타입은 number 이지만 숫자가 아닌 값이 된다.


### string

'123' : 문자열

"ABC" : 문자열

string 은 따옴표('), 쌍따옴표(") 둘다 사용 가능하다.

> 개인적으로는 따옴표를 주로 사용한다.  
> 문자열안에 쌍따옴표를 넣는 경우가 더 많은 것 같은 느낌(?) 때문에


\`문자 안에 스크립트를 넣고 싶을때 \` : ES6 부터 사용가능

\`10 + 10 = ${10 + 10}\` : 10 + 10 = 20



### symbol()

고유한 값을 만들고 싶을때 사용

```js
const a = Symbol('Const');
const b = Symbol('Const');

console.log(a === b);

typeof a; // "symbol"
```

a와 b 는 값은 값을 넣은 것 처럼 보이지만 같지가 않다.

symbol 은 new 로 만들 수 없다.

ES6 부터 사용가능

```js
new Symbol(); // error
```
