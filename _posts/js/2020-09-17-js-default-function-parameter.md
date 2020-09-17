---
title: "default function parameter - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-17T20:20:00
---

# default function parameter - call) 기본값 매개변수

> ES6

함수의 파라미터가 없거나 `undefined`을 경우 해당 파라미터에 기본값을 넣어 초기화 시킬 수 있다.

```js
function (a, b = 1) {
  return a + b + 10;
}

(a, b = 1) => a + b + 10;
```
