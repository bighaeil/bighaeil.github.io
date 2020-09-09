---
title: "Arrow Function - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-09T20:10:00
---

# Arrow Function - ES6

function 도 길다.

ES6 에서는 function 을 생략하고 화살표로 함수를 만들 수 있다.

```js
const _add = function(a, b) {
  return a + b;
}

const add = (a, b) => {
  return a + b;
}

const add2 = (a, b) => a + b;/
```

위 `_add` 와 `add` 함수는 같은 함수이다.

그리고 `add` 함수 처럼 함수 내부에서 바로 어떤 값을 return 하는 경우에

`add2` 처럼 더 간단하게 작성할 수 있다.

그리고

화살표 함수의 경우 `this` 는 상위 객체를 가리키게 되는데 이는 객체를 다룰 때 알아보자.
