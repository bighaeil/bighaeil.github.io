---
title: "spread & rest - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-20T20:10:00
---

# spread

spread는 `펼치다` 라는 뜻이다.  
객체의 속성을 펼칠 수 있다.  

```js
const cafe = {
  coffee: 'Americano'
};

const secondCafe = {
  ...cafe,
  bread: 'Sandwich'
};

cafe; // { coffee: 'Americano' }
secondCafe; // { coffee: 'Americano', bread: 'Sandwich' }
```

spead 연산자(...)을 사용하면 cafe의 속성이 펼쳐지게 된다.  
그래서 coffe의 속성이 secondCafe에 들어가게 된다.  

보통 속성을 넣을때 점 연산자(.)를 사용하니까  
속성을 넣는 것이라면 다음과 같이 해도 되지 않을까?

```js
const cafe = {
  coffee: 'Americano'
};

const secondCafe = cafe;
secondCafe.bread =  'Sandwich';

cafe; // { coffee: 'Americano', bread: 'Sandwich' }
secondCafe; // { coffee: 'Americano', bread: 'Sandwich' }
```
위 연산은 secondCafe라는 변수에 cafe 객체를 참조하는 한다.  
즉 cafe와 secondCafe는 같은 객체이다.  
그래서 secondCafe에 속성을 넣는 것은 곧 cafe에 속성을 넣는 것이 된다.  

그 결과 spead와 같은 결과를 얻을 수 없다.

## deep copy - call) 깊은 복사

위 같은 성격으로 깊은 복사를 구현할 수 있는데  

> 모든 속성의 값이 `object`가 아닌 경우

```js
const target = {
  coffee: 'Americano',
  bread: 'Sandwich'
};

const deepCopy = {
  ...target
};

target === deepCopy; // false
```

## spread 시  중복 속성이 존재하는 경우

만약 A 객체에서 B 객체로 spread 하는 경우 중복된 값이 존재한다면 어떻게 될까?

```js
const A = {
  a: 1,
  b: 2,
  c: 3
}

const B1 = {
  ...a,
  b: 20
}

const B2 - {
  b: 20,
  ...a
}

b1; // { a: 1, b: 2, c: 3 }
b2; // { a: 1, b: 2, c: 3 }
```

spread 연산 후 b 속성이 있는 경우(b1)와 b 속성이 있고 spread 연산을 하는 경우(b2)를 확인하면 중복되는 속성(b)이 a의 속성(b)으로 되는 것을 확인 할 수 있다.  

즉 b의 객체에 a의 속성을 넣는 것으로 볼 수 있겠다.

```js
B1.b = A.b;
B2.b = A.b;
```

## array spread

배열도 역시 spread 연산자가 가능하다.

```js
const a = [1, 2, 3];
const b=  [4, 5];

[...a, b]; // [1, 2, 3, 4, 5]
[...a, b, ...a]; // [1, 2,3, 4, 5, 1, 2, 3]
```
spread 연산을 2번 사용할 수 도 있다.

# rest

`rest`는 나머지라는 뜻이다.  
그래서 객체 속성의 나머지를 표현한다.  
즉 객체나 배열이나 파라미터 등에 나머지를 표현할 때 사용한다.
`rest`도 spread 처럼 `...`을 사용한다.  

```js
const obj = {
  a: 1,
  b: 2,
  c: 3
}

const { c, ...rest } = obj;
c; // 3
rest; // { a: 1, b: 2}

const { b, ...rename } = obj;
c; // 2
rename; // { a: 1, c: 3}
```

구조 분해 할당을 통해 속성을 전제하는데 속성 c만 사용하고 나머지는 rest라는 object에 넣었다.  

여기서 spread 연산자의 경우는 객체의 속성을 퍼트렸다면 여기서 `rest`로 사용한 spread 연산자는 나머지 속성들을 모아주는 역할을 했다.

여기서 rest는 rest 연산자라서 사용한 것이 아니고 그냥 이름이라는 사실이다. 원하는데로 지어도 상관없다.

rest 배열에서도 사용할 수 있다.

```js
const arr = [1, 2, 3, 4, 5];
const [one, two, ...rest] = arr;

one; // 1
two; // 2
rest; // [3, 4, 5]
```
이때의 `rest`는 가장 마지막에서만 사용할 수 있다는 것을 알아두자.

# function rest

함수에서도 rest를 사용할 수 있다.

```js
const fn = function ({ a, ...rest }) {
  a;
  rest;
}

fn(1, 2, 3, 4, 5);
// a: 1
// rest: [2, 3, 4, 5]
```

fn의 첫번째 파라미터 a는 첫번째 인자(1)가 들어가고 나머지는 rest안에 배열[2, 3, 4, 5]로 들어간다.

> 파라미터 : 함수가 받는 괄호 안의 변수들  
> ex) function abc(a, b, c)

> 인자 : 함수를 실행할때 넣는 값들  
> ex) abc(1, 2, 3)

함수의 인자를 `spread`로 넣을 수 있다.

```js
const arr = [1, 2, 3, 4, 5];
const abc = function(a, b, c, d, e) {
  //
}

abc(...arr);
```

abc의 파라미터를 저런 식으로 넣는게 썩 마음에 들지 않지만 그냥 예시로 보면될 것 같다.  
