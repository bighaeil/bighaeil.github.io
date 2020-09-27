---
title: "prototype - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-16T20:00:00
toc: true
toc_sticky: true
---

# prototype - call 프로토타입

## 객체 생성자

함수 선언하여 객체로 만들 값 또는 함수를 넣는다.  
`new` 라는 키워드를 사용하여 객체(joe, ani)를 만든다.  

```js
function Human(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.move = function() {
    // do
  }
}

const joe = new Human('joe', 20);
const ani = new Human('ani', 30);
```

객체를 생성할 때는 보통 이름의 첫 글자는 대문자(Human)를 사용한다.  
객체의 프로토타입(prototype)으로 속성과 메소드를 `상속`할 수 있다.

> 상속이라 표현한 이유는 모든 객체는 `Object`의 인스턴스로서 Object.prototpye을 통해서 속성과 메소드를 넣은 것이기 때문이다.

```js
function Human(name, age) {
  this.name = name;
  this.age = age;
}

Human.prototype.move = function() {
  this.name;
}

Human.prototype.job = 'person';
```

함수(move)는 밖에서 `prototype`으로 만들 수 있다.  
`prototype`은 객체 생성자로 객체를 만들었을 때 객체들이 사용할 수 있는 속성과 메소드를 주입할 수 있다.


# 상속

만약 직업을 표현하는 객체 2개를 선언한다고 했을 때
```js
function Seller(name, age) {
  this.name = name;
  this.age = age;
  this.job = 'seller';
}

function Buyer(name, age) {
  this.name = name;
  this.age = age;
  this.job = 'buyer';
}

const seller = new Seller('joe', 20);
const buyer = new Buyer('ani', 30);
```

두 객체는 거의 비슷한데 두번이나 작성해야 한다.  
두 객체를 보면 보통 사람(Human)과 같은 공통적인 특징(name, age, job)이 존재한다.  
최대한 Human이 가지고 있는 특징을 재사용 해보자.

```js
function Human(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
}

function Seller(name, age) {
  Human.call(this, name, age, 'seller');
}

function Buyer(name, age) {
  Human.call(this, name, age, 'buyer');
}

Seller.prototype = Human.prototype;
Buyer.prototype = Human.prototype;

```

`Seller`와 `Buyer`는 `Human`의 멤버를 상속받도록 했다.  
`call` 메소드를 사용해 다른 객체에 멤버를 상속할 수 있다.  
이 때 `this`는 현제 객체(호출하는 객체 - Seller, Buyer)를 가리킨다.
