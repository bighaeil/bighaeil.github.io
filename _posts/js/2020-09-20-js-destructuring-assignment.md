---
title: "Destructuring assignment - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-20T20:00:00
toc: true
toc_sticky: true
---

# Destructuring assignment - call) 구조 분해 할당

`구조 분해 할당`은 배열이나 객체의 숙성을 해제하여 그 값을 개별 변수에 담을 수 있게 하는 문법이다.

```js
const obj = { a: 1, b: 2};

function fn({a, b, c = 3}) {
  a;
  b;
  c;
}
```

구조 분해 할당을 통해 a와 b를 분해했고 추가로 존재하지 않는 c를 초기화해서 c가 없을 경우 c는 3으로 초기화 한다.

## 이름 변경

만약 구조 분해 할당을 할때 꼭 같은 이름으로 해야 하는가  
그건 아니다.

```js
const obj = { a: 1, b: 2};

const { a: name } = obj;

name; // 1
```

구조 분해하는 변수에 오른쪽에 이름(name)을 추가해서 변경할 수 있다.  
그렇닥도 a의 이름이 변경되는 것은 아니다.

## 배열 구조 분해 할당

배열도 역시 구조 분해를 할 수 있다.

```js
const arr = [1, 2];

const [val1, val2, val3 = 3] = arr;

val1;
va2l;
```

중괄호({})를 대괄호([])로 바꾸면 배열 구조 분해 할당이 된다.


## 깊은 구조 분해 할당

복잡한 구조의 경우 구조 분해 할당을 해보자.

1. 구조 분해를 중복해서 사용하는 방법

```js
const obj = {
  state: {
    info: {
      name: 'joe',
      skill: ['reading', 'singing']
    }
  },
  value: 100
}

const { name, [first, second] } = obj.state.info;
const { value } = obj.value;

name;
first;
second;
value;
```

depth 가 2단계인 info와 1단계인 value를 따로 가져온다.

2. depth를 탐색하면서 가져온다.

```js
const {
  state: {
    info: {
      name,
      skill: [first, second]
    }
  },
  value
} = obj;

name;
first;
second;
value;
```

첫번째 보다 보기가 힘들어지는 것은 사실인다. 이렇게 할 수 도 있다는 것만 알아두자.  
