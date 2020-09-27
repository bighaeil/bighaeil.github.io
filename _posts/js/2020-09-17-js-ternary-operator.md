---
title: "Ternary Operator - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-17T20:00:00
toc: true
toc_sticky: true
---

# Ternary Operator - call) 삼항연산자

> condition ? true : false

조건이 true 이면 `true`를 실행하고  
조건이 false 이면 `false`를 실행한다.

```js
if (a === 10) {
  a + 10;
} else {
  a;
}

a === 10 ? a + 10 : a;
```

if문을 사용하면 많은 줄을 사용하는데 삼항연산자를 사용하면 간단히 만들 수 있다.  
생각보다 참인지 거짓인지만 판단해야하는 경우가 많기 때문에 유용한다.

만약 조건과 결과가 길다면 다음과 같이 쓸 수도 있다.
```js
a === 10 ?
  a + 10 :
  a;
// or

a === 10
  ? a + 10
  : a;
```

취향에 따라서 보기 좋은 걸 선택하면 되겠다.

삼항연산자를 중첩해서 사용할 수도 있다.
```js
a ? 'A' : b ? 'B' : 'C';
// or
!a ? b ? 'B' : 'C' : 'A';
```

보면 알겠지만 오히려 햇갈리는 부분이 더 많아진다.  
그래서 한번만 사용하는 것을 추천한다.  
