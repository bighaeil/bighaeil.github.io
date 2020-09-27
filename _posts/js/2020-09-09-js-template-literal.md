---
title: "Template Literal - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-09T20:00:00
toc: true
toc_sticky: true
---

# Template Literal - ES6

> `ES6`란 ECMAScript 6 를 의미하며 자바스크립트 버전을 의미한다.  
> 2015 년에 나와서 ES2015 라고도 한다.  
> ES5 에서 ES6 로 넘어오면서 많은 것이 바뀌였는데 전부 알 필요는 없고  
> 필요한 것 위주로 알고 나머지는 찾아보면 되겠다.  

예전 버전에서 string 을 합치고 싶으면

```js
var world = 'World!';
var str = 'Hello' + ' ' + world;
```

`+` 를 계속 넣어야 했는데

`Template Literal`을 사용하면 간단하게 줄이 수 있다.

```js
var world = 'World!';
var str = `Hello ${world}`;
```

`${}` 안에 연산식을 넣거나 변수를 넣어 `+`를 생략하고 문자열을 만들 수 있다.
