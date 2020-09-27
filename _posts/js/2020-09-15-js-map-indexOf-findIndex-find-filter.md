---
title: "map, indexOf, findIndex, find, filter - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-15T20:10:00
toc: true
toc_sticky: true
---

# map

배열을 변환하고 싶을 때  
바꾸고 싶을 때 사용하는 내장 함수

```js
const arr = ['A', 'B', 'C', 'D'];

const newArr = arr.map(word => {
  return word + word;
}); // ['AA', 'BB', 'CC', 'DD']

```

해당 배열을 변환시킨 새로운 배열을 만든다.  
즉 새로운 배열을 반환한다.

# indexOf

특정 항목이 배열의 몇 번쩨 항목인지 찾아주는 내장 함수

```js
const index = arr.indexOf('B'); // 1
```
일치하지 않은 경우 `-1`을 반환한다.

하지만 특수한 항목 예를 들면 객체의 특정 값은 찾을 수가 없다.

# findIndex

특정 조건을 확인해서 일치하는 경우 몇 번째 항목인지 알려주는 내장 함수

```js
const objs = [
  {
    id: 1,
    text: 'A'
  },
  {
    id: 2,
    text: 'B'
  },
  {
    id: 3,
    text: 'A'
  },
];

const index = objs.findIndex(obj => obj.id === 3); // 2
```

# find

`findIndex`와 비슷하지만 index가 아니고 객체 자체를 반환 한다.

```js
const target = objs.findIndex(obj => obj.id === 3); // { id:3, text: 'A' }
```

# filter

특정 조건을 만족하는 원소를 찾아서 새로운 배열을 만드는 내장 객체

```js
const newObjs = objs.filter(obj => obj.text === 'A');
// [{ id:1, text: 'A' }, { id:3, text: 'A' }]
```


