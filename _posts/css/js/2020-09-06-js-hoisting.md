---
title: "hoisting - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-06T21:00:00
---

# hoisting - call) 호이스팅

[hoisting](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)

호이스팅의 뜻을 끌어올린다는 의미이다.

예제를 먼저 살펴보자

함수를 선언 후 사용
```js
function hello() {
  console.log('Hello');
}

hello();
```

함수 호출을 먼저하고 함수를 선언
```js
hello();

function hello() {
  console.log('Hello');
}
```

js 에서는 두 경우 모두 문제없이 사용할 수 있다.

이유는 호이스팅 형상때문에 아래 있는 선언을 끌어올려서 사용하기 때문에

그래서 마치 오류처럼 보이는 코드가 문제없이 동작하게 된다.

> 이런 현상은 문제없이 동작하니 도움을 주는 것 처럼 보이지만
> 실제 코드를 작성하고 동작할때 예측하기 어렵거나 원하지 않는 동작을 야기하게 된다.

즉 js 의 특징으로 호이스팅을 이해하고 적극적으로 사용하지는 않지만 호이스팅이 일어나면 어떤 원인인지 파악할 수 있어야 한다.

