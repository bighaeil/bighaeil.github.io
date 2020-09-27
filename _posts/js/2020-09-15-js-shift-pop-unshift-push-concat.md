---
title: "shift, pop, unshift, push, concat - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-15T20:30:00
toc: true
toc_sticky: true
---

# shift

배열의 첫번째 항목이 빠져나온다.  
즉 원본 배열이 수정된다.  

배열이 비여있어도 오류 없이 계속 뺀다.  
단지 `undefined`가 나온다.  

```js
const arr = ['A', 'B', 'C', 'D'];

const value = arr.shift(); // 'A'
arr; // ['B', 'C', 'D']
```

# pop

배열의 마지막 항목이 빠져나온다.  
즉 원본 배열이 수정된다.  

배열이 비여있어도 오류 없이 계속 뺀다.  
단지 `undefined`가 나온다.  

```js
const arr = ['A', 'B', 'C', 'D'];

const value = arr.pop(); // 'D'
arr; // ['A', 'B', 'C']
```

# unshift

배열의 앞에 새로운 항목을 넣는다.  
즉 원본 배열이 수정된다.  

```js
const arr = ['A', 'B', 'C', 'D'];

arr.unshift(10);

arr; // [10, 'A', 'B', 'C', 'D']
```

# push

배열의 마지막에 새로운 항목을 넣는다.  
즉 원본 배열이 수정된다.  

```js
const arr = ['A', 'B', 'C', 'D'];

arr.push(20);

arr; // ['A', 'B', 'C', 'D', 20]
```

# concat

두 배열을 하나로 합친다.

```js
const arr1 = [1, 2, 3];
const arr2 = ['A', 'B', 'C'];

const newArr = arr1.concat(arr2); // [1, 2, 3, 'A', 'B', 'C']
```

원본 배열을 바꾸지 않고 새로운 배열을 반환한다.

# join

배열을 새로운 문자열 형태로 반환한다.  
이때 구분할 문자(seperator)를 넣을 수 있다.

```js
const arr1 = [1, 2, 3];

const str1 = arr1.join(); // 1,2,3
const str2 = arr1.join(', '); // 1, 2, 3
```

`join`에 `seperator`를 넣지 않으면 기본 seperator 콤마(,)를 넣는다.  
 join은 마지막 항목에는 자동으로 seperator를 넣지 않기 때문에 구분해서 넣기 아주 편리하다.

 