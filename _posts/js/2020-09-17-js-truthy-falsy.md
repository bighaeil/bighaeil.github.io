---
title: "Truthy & Falsy - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-17T20:10:00
---

# Truthy & Falsy

javascript에서는 참으로 판단하는 값과 거짓으로 판단하는 같이 존재하기 때문에 햇갈릴 수 있는 부분이 있다.

javascript에서는 `null`과 `undefined`가 동시에 존재한다.  
null은 값이 없다는 의미이고
undefined는 정의되어 있지 않다는 의미이다.  

비슷해 보이지만 조금씩 다르기 때문에 햇갈릴 수 있다.  

그래서 값의 상태를 구분해서 찾는 것보다는 참인 것과 거짓은 것으로 판단하는 것이 소스가 명확해 진다.

```js
const person; // null 이던지 undefined 던지

person.name; // error

if (person) { // null check;
   person.name; // not working
}
```

person은  `undefined` 상태로 정의되어 있지 않다. 그런 person을 사용하려고 하면 **error**를 내뱉는다.  
그래서 pserson 이 Falsy 한 특징을 활용하여 조건문으로 에러를 체크할 수 있겠다.


## Truthy

javascript에서 참인 값으로 판단하는 것

```js
3; // 영이 아닌 숫자
'hello'; // 뭔가 들어있는 문자
[]; // 빈 array
{}; // 빈 object
```

주의해야할 부분은  
왠만하면 값이 있으면 모두 참이라는 것이다.  
그런데 `[]`나 `{}`는 눈으로 보기에는 아무것도 없어서 거짓같아 보이지만 사실 참이라는 것이다.  
`[]`나 `{}`는 둘 다 `object`로 어딘가 객체가 메모리에 존재한다.  
그렇기 때문에 참이다.


## Falsy

javascript에서 거짓인 값으로 판단하는 것

```js
undefined; // 정의되지 않음
null // 값이 없음
0; // 숫자 영
''; // 빈 문자
NaN; // 숫자이지만 숫자가 아님
false; // 거짓
```

주의해야할 부분은  
`0`이나 `''`같은 값이 존재하지만 Falsy한 값들은 실재로 사용할 수도 있으니 if문을 활용할때 조심해야겠다.  


## check Truthy or Falsy

이 값이 Truthy한지 Falsy한지 알고 싶으면 다음과 같이 작성해보자 참인지 거짓인지 알 수 있다.

```js
const a = {};

!!a ? true : false;
```

값에 `!` 논리 연산자를 붙이면 `boolean` 형태로 해당 값의 반대를 반환하는 것을 사용하여  
`!`를 2개 붙여서 boolean 값을 확인할 수 있다.


# short-circuit evaluation - call) 단축 평가 논리 계산법

논리 연산자의 `and`와 `or`을 확인해보자.

```js
if (a && b && c) {}

if (a || b || c) {}
```

`&&` 연산자는 and 논리 연산자로 해당 조건(a, b, c)이 모두 `true`여야 참을 반환한다.  
(참을 반환하면 조건문에 들어간다는 의미)  
그러므로 a가 만약 false 라면 b, c 조건은 확인하지 않아도 전체 조건은 false이기 때문에 b와 c는 생략된다.  

이를 `단축 평가 논리 계산법`이라 한다.

마찬가지로 `||` 연산자는 or 논리 연산자로 해당 조건(a, b, c)이 하나라도 `true`여야 참을 반환한다.  
그러므로 a가 만약 true 라면 b, c 조건은 확인하지 않아도 전체 조건을 true이기 때문에 b와 c는 생략된다.

이를 활용하면 특정값이 유효한지 안한지 체크하면서 연산을 작성할 수 있다.

```js
const person; // 값은 있을 수도 없을 수도 있다.

//...

if (person && person.name === 'joe') {  

}
```

코드가 길어지거나 데이터를 가져올때 값은 있을 수도 없을 수도 있다.  
person이 존재한다고 확인할 수 있으면 person.name을 확인할 수 있겠지만 그렇게 자신할 수 있는 경우는 많지 않을 것이다.  
그럴때는 앞에 person이 존재하는지 먼저 체크해서 false라면  
에러는 뱉는 person.name은 연산하지 않고 바로 조건문을 종료할 수 있다.

이런 조건은 연산은 상당히 많이 활용하기 때문에 꼭 알아 두어야 한다.
