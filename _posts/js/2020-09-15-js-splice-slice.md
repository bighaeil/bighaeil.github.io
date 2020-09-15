---
title: "splice, slice - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-15T20:20:00
---

# splice

배열에서 특정 항목을 제거하는 내장 함수  
배열 자체에서 항목을 제거하고  
제거한 항목의 index를 반환한다.
즉 원본 배열의 항목이 삭제된다. 

> Array.splice(선택_인덱스, 삭제한_항목의_수);

```js
const arr = ['A', 'B', 'C', 'D'];

const index = arr.indexOf('B');

const removed = arr.splice(index, 2);

```

# slice

배열에서 `start index`부터 `end index`전 까지 잘라서 새로운 배열을 반환하는 내장 함수  
즉 원본 배열은 건드리지 않는다.  
자른 부분을 반환한다.  
`end index` 포함이 아니고 전까지라는 것을 기억하자

```js
const arr = ['A', 'B', 'C', 'D'];

const sliced = arr.slice(1, 3); // ['B', 'C']
arr; // ['A', 'B', 'C', 'D']
```
