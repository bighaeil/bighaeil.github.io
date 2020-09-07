---
title: "conditional-statements - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-07T20:10:00
---

# Conditional Statements

## if

표현식이 참으로 평가될 때 실행되는 블럭

```js
if (true) {
  // 실행
}

if (false) {
  // 실행되지 않음
}
```

블럭을 쓰지 않으면 한줄로 표현가능

```js
if (true) console.log("true");
```

### true

[Truthy](https://developer.mozilla.org/ko/docs/Glossary/Truthy)

표현식이 거짓으로 평가되는 경우는 제외하고 모든 경우는 true 이다.

* Falsy 의 반대
  * true
  * 37 : 0을 제외한 number
  * 'string' : 빈 문자열을 제외한 문자열
* {} : object
* [] : array - 결국은 object

### false

[Falsy](https://developer.mozilla.org/ko/docs/Glossary/Falsy)

표현식이 거짓으로 평가되는 경우

* false
* 0
* '' or ""
* null
* undefined
* NaN

## else 

if 가 아닌 때 실행

```js
if (false) {
  // not run
} else {
  // run
}
```

## else if 

if 가 아닌 경우 다음 조건이 참으로 평가될 때

```js
var n = 10;

if (n < 5) {
  // not run
} else if (n > 5) {
  // run
} else {
  // not run
}
```

else if 는 여러개를 넣을 수 있다.

## 논리 연산자

### && - call) and 연산자

and 연산자

```js
if (false && false) {
  // not run
} else if (false && true) {
  // not run
} else if (true && true) {
  // run
}
```

`&&`로 연결된 조건들 중에 하나라도 `false` 인 경우 연산결과는 `false`

### || - call) or 연산자

or 연산자

```js
if (false && false) {
  // not run
} else if (false && true) {
  // possible run
} else if (true && true) {
  // possible run
}
```
`||`로 연결된 조건들 중에 하나라도 `true` 인 경우 연산결과는 `true`

### ! - call) not 연산자

not 연산자

```js
if (!true) {
  //not run
} else if (!false) {
  //run
}
```

조건문 앞에 `!`가 붙으면 연산결과의 반대가 된다.

## 조건부 실행

위의 조건부 연산자는 각 특징을 가지고 있다.

`&&` : 하나라도 false 면 결과는 false  
`||` : 하나라도 true 면 결과는 true

즉 먼저 연산한 조건식에 따라서 뒤에 나오는 조건식들은 연산하지 않을 수 있다.

```js
var condition1 = false;
var condition2 = false;
var condition3 = true;

if (condition1 && condition2 && condition3) {
  // not run
}

```

and 연산에서 이미 `condition1`가 false 이기 때문에  
`condition2` 와 `condition3` 은 연산하지 않는다.

마찬가지로

```js
var condition1 = true;
var condition2 = false;
var condition3 = true;

if (condition1 && condition2 && condition3) {
  // run
}

```

or 연산에서 `condition1`이 이미 true 이기 때문에  
`condition2`와 `condition3`은 연산하지 않는다.

즉
```js
var emptyObject;

if (emptyObject && emptyObject.property) {
  // not run
}
```

`emptyObject`는 undefined로 객체(object)의 속성(property) 찾으려는 연산을 수행하면  
에러가 발생하지만
and 연산에 의해 이미 앞쪽에서 false 라는 결과가 나왔기 때문에  
뒤의 연산을 수행하지 않는다.  
즉 에러가 발생하지 않는다.


## 삼항 연산자

블럭({})을 사용하지 않는 문법으로

```js
조건 ? "조건이 참이면 실행되는 표현식" : "조건이 거짓이면 실행되는 표현식";
```

## switch

`switch` 뒤 괄호안 값이 무엇인지 `case` 값들과 비교해서 실행한다.  
`default` 키워드는 어떤 값에 상관없이 실행된다.  

```js
switch(2) {
  case 1:
  console.log(1); // not run
  break;
  case 2:
  console.log(2); // run
  break;
  case 3:
  console.log(1); // not run
  break;
  default:
  console.log(0); // not run
}
```

switch문 step

1. 2를 첫 case 1과 비교한다.
2. 같지 않기 때문에 넘어간다.
3. 다음 2와 case 2를 비교한다.
4. 일치한다.
5. console에 2를 찍는다
6. break 에 의해 swtch 문이 종료한다.

만약 break 가 없는 경우

```js
switch(2) {
  case 1:
  console.log(1); // not run
  case 2:
  console.log(2); // run
  case 3:
  console.log(1); // run
  default:
  console.log(0); // run
}
```

1. 2를 첫 case 1과 비교한다.
2. 일치하지 않기 때문에 넘어간다.
3. 다음 2와 case 2를 비교한다.
4. 일치한다.
5. console에 2를 찍는다
6. console에 3를 찍는다 - break 를 만나기 전까지 이후 코드들은 모두 실행한다.
7. default 는 어떠한 값에 상관없이 싱행한다.
8. console에 0을 찍는다
9. switch 문을 종료한다.

break 는 필수가 아니기 때문에 필요에 따라 사용할 수 있지만  
위처럼 불명확한 요소가 존재하기 때문에 조심해서 사용해야 한다.  
