---
title: "Hoisting - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-20T20:30:00
---

# Hoisting - call) 호이스팅

`hoisting`의 뜻은 '끌어올린다' 이다.  
호이스팅은 선언되지 않은 함수나 변수를 끌어볼려서 사용할 수 있도록하는 것이다.  

```js
fn(); // 1번

function fn() {
  // run
}

fn(); // 2번
```

함수 2번의 경우 위에 fn이 선언되어 있고 fn을 실행했기 때문에 자연스럽게 실행될 것이라고 예측할 수 있다.  
그러나 1번 fn은 마치 먼저 실행하고 선언한 것 처럼 보여서 부자연스럽게 보이지만 javascript에서는 `호이스팅`이란 처리가 있어서 마치 2번처럼 동작하게되어 실행하는데 문제가 없다.  

이것은 javascript의 특징이긴 하지만 개발자가 보기에는 엄청 햇갈리게 만들 수 있는 요지가 생긴다. 그래서 `호이스팅`은 피해야 한다.

변수도 마찬가지로 `호이스팅`이 된다.

```js
console.log(number); // error
```

number는 없기 때문에 에러가 나는 것이 당연하다.

```js
console.log(number); // undefined
var number = 2;
```

이때 number는 undefind로 어디에도 선언된 적이 없는데 문제없이 동작한다. 이는 아래에 var로 선언된 number가 `호이스팅`되어 없는 number가 끌어올려진 것이다.  

만약 var를 let으로 바꾼다면?

```js
console.log(number); // error
let number = 2;
```

number는 선언되어 있지 않기 때문에 정상적으로 에러가 난다.  

`호이스팅`은 깜빡할 수 있는 선언을 끌어올려줘서 마치 코딩을 도와주는 것처럼 보이지만 실상은 개발자로 하여금 엄청 햇갈리게 만드는 요소이기 때문에 사용하지 않는 것을 추천한다.  

만약 이런 실수할 수 있는 코드를 방지하고 싶으면

`ESLint` 같은 tool을 사용하면 되겠다.  

> `ESLint` : javascript 코드에서 발견된 문제 패턴을 식별해주는 정적 코드 분석 도구
