---
title: "Expression - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-06T20:10:00
---

# Expression

값을 만들어내는 표현을 표현식(Expression) 이라함

ex)  
```js
100 + 100  
"Hello"  
```


값을 만들어내기 때문에 함수(function)의 인자(parameter)로 사용할 수 있다.

ex)  
```js
alert("Hello" + "World!");  
```

# Statement

하나 혹은 여러 개의 표현식이 모여서 문장(statement)을 이룸

모든 표현식은 문장이 될 수 있다.

문장의 끝에는 세미콜론(;)을 붙인다 - js 에서는 안붙일 수도 있지만... - 관례적으로 붙인다.

조건문의 {} 뒤에는 세미콜론을 붙이지 않는다.

ex)  
```js
true;  
100 + "Hello";
```
