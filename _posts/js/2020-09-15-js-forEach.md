---
title: "forEach - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-15T20:00:00
---

# forEach

배열의 목록을 조회할 수 있는 배열 내장함수

```js
const arr = ['A', 'B', 'C', 'D'];

const print = function(word) {
  word;
}

arr.forEach(print);

arr.forEach(function(word) {
  word;
});

arr.forEach(word => {
  word;
});
```

배열의 목록을 조회하면서 일관된 작업을 하고 싶으면  
`forEach` 내장 함수를 사용하면 된다. 해당 인자로 함수를 넣으면되고  
그 함수의 파라미터에는 value를 담을 변수를 넣으면 된다.

