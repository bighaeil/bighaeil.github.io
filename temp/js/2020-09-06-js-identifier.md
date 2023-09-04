---
title: "Identifier - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-06T20:30:00
toc: true
toc_sticky: true
---

# Identifier

코드 내의 변수, 함수, 속성을 식별하는 문자열

ex)  
```js
var name = "Jon";  
function hello() {}  
var person = {  
  name: 'anna',
  age: 20
}
```

## naming

유니코드 문자(한글 가능 - 하지만 사용하지 않음), $, _, 숫자(0,-9)를 사용할 수 있다.

숫자로 시작 할 수 없다.

예약어는 사용할 수 없다.

공백(space)를 사용할 수 없다.

ex)
```js
var name;
var $name;
var _age;
var 이름; //사용할 수 있지만 사용하지 않음
```

이름 짓기는 가장 어려운 일임

의미없는 이름을 사용하지 말고 역할에 맞는 적절한 이름을 짓도록 해야한다.

