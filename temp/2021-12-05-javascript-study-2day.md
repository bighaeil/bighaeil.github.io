---
title: "JAVASCRIPT STUDY FUNCTDION"
categories:
    - study
last_modified_at: 2021-12-08T12:35:00
toc: true
toc_sticky: true
---

# FUNCTDION

함수는 보통 무언가를 받아서 처리하고 결과를 반환하는 절차로 사용합니다.

하지만 javascript에서는 조금 더 특별합니다.

javascript funtion은 다른 모든 객체처럼 속성과 메서드를 가질 수 있는 `객체`입니다.

이를 염두하고 함수에 대해서 알아보겠습니다.


## 함수 표현식

```js
var f1 = function () {
}
function f2 () {
}
```

### 이름없는 함수 vs 이름있는 함수

함수 f1은 이름없는 함수를 선언하여 변수 f1에 할당한 형태입니다.

물론 아래처럼 선언할 수 있습니다.

```js
var f = function f1() {
}

f(); // possible
f1(); // error
```

이름있는 함수 f1을 선언하여 변수 f에 할당했지만 f1은 함수로 사용할 수 없습니다.

이름있는 함수는 __함수의 범위 안에서만 사용할 수 있습니다__. 여기서 f1은 변수안에 선언되어 범위가 한정된 것으로 보입니다. 그래서 에러를 발생하고 있습니다. 

결론적으로 이름있는 함수는 되도록 사용하지 않습니다. 또한 함수 범위가 모호해지기 때문에 뒤에서 알아볼 Hoisting 때문에라도 사용하지 않습니다. 


## 화살표 함수(arrow funtion)

```js
const f1 = () => {
  return 1;
}
const f2 = () => 1; 
```

전통적인 함수표현의 간단한 표시입니다.

그렇다고 완전히 기존 function과 같지는 않은 것 같습니다.

1. this나 super에 대한 바인딩이 없습니다.
2. new 키워드가 없습니다. prototype 도 없습니다.
3. 스코프를 지정할 때 사용하는 메소드를 사용할 수 없습니다.
4. 생성자로 사용할 수 없습니다.
5. yield를 사용할 수 없습니다. (yield는 제너레이터 함수에서 사용하는 키워드 인데 기회가 되면 설명하겠습니다.)

화살표 함수의 특징은 간단한 표시이외에도 중요한 특징이 있습니다.


### 화살표 함수와 this

기존 function은 이 함수가 어디서 호출되는지에 따라 자신의 this를 정의했습니다.

```js
function Person() {
  this.age = 0;
  
  setInterval(function growUp() {
    this.age++; // this === window
  }, 1000);  
}
var p = new Person();
```

위 에서 Person은 age라는 멤버를 가지고 있어서 1초마다 증가시키려고 하지만 동작하지 않습니다. 이때 사용한 growUp 함수는 this를 전역 객체(여기서는 window)로 정의하고 있기 때문입니다. 즉 Person 안에서 growUp 함수를 선언한 것 처럼 보이지만 사실은 아닙니다.

여러가지 해결방법(바인딩 등)이 있겠지만 화살표 함수로 해결할 수 있겠습니다.

```js
function Person() {
  this.age = 0;
  
  setInterval(() => {
    this.age++; // this === Person의 인스턴스
  }, 1000);  
}
var p = new Person();
```

화살표 함수는 this가 없습니다. 대신 화살표 함수를 둘러싸는 렉시컬 범위(쉽게 scope)의 this를 사용됩니다. 현재 범위에서 this가 존재하지 않을 때는 바깥에서 this를 찾습니다.

---

개인적으로 function에서 this가 중요하다고 생각합니다. 이유는 javascript에서 function은 객체이기 때문에 현재 진행하는 동작이 누구인지가 중요하기 때문입니다.


## Object

먼저 간단하게 오브젝트를 만들어 보겠습니다.  
(인스턴스라고 불러야될지는 모르겠습니다. 보통 인스턴스는 설계도를 바탕으로 구현된 구체적인 실체라는 의미를 가지기 때문에 javascript의 객체도 마찬가지인지는 확인이 필요합니다.)


```js
var obj = {
  name: '123',
  fn: function () {
    return this.name;
  }
};

obj.fn(); // '123'

var obj2 = new obj();

obj2.fn(); //error: obj is not constructor
```

javascript에서 오브젝트는 중괄호`{}`를 이용하여 쉽게 실체가 있는 객체로 만들 수 있습니다. 하지만 이 객체는 설계도`class`없이 만들었기 때문에 `new`키워드를 이용하여 객체를 만들 수 없습니다. 
obj에는 속성 name이 있습니다. 속성 fn은 함수로 무언가를 실행하는데 이때 동작을 하는 주체`this`는 자기 자신이 됩니다.

ES5 기준으로 javascript에는 `class` 키워드가 없습니다. 그래서 이전에는 `function`을 사용하여 객체를 만들었습니다.


```js
function Person(name) {
  this.name = name;
  this.age = 1;
  this.fn = function () {
    return this.name;
  }
}

var baby1 = new Person('철수');

baby1.fn(); // '철수'

var baby2 = new Person('영희');
```


Person이라는 설계도를 이용하여 객체를 설계하고 `new`키워드를 이용하여 인스턴스를 생성했습니다.
Person 안에 this는 객체 자기 자신을 가리킵니다. 그리고 function 안의 this 역시 자기 자신을 가리킵니다.

Object() 생성자를 이용한 객체 생성도 있지만 생략하겠습니다.


### prototype과 상속 

javascript는 프로토타입 기반 언어(prototype-based language)라고 불립니다. 그만큼 프로토타입을 이해하는 것이 필수라고 생각합니다. (그만큼 어렵기도 합니다.) 프로토타입은 모든 객체를 상속하기 위해 프로토타입 방식을 사용합니다. 자식은 부모의 프로토타입을 상속 받을 수 있고, 그 부모 역시 부모의 프로토타입을 상속받을 수 있습니다. 이를 프로토타입 체인(prototype chain)이라 합니다.


```js
function Person() {
  this.name = 'self';
}
Person.prototype.name = 'parent';

var boy = new Person();
console.log(boy.name); // self
console.log(boy.__proto__.name); // 'parent'
```


```js
function Teacher() {
}
Teacher.prototype = Person;

var man = new Teacher();
console.log(man.name); // 'parent'
```


관리자모드에서 위 코드를 실행하면 아래와 같은 화면을 확인할 수 있습니다.

![object](//bighaeil.github.io/assets/images/2021-12-14_object.png)

![inheritance](//bighaeil.github.io/assets/images/2021-12-14_inheritance.png)

Person 안에는 name이라는 속성이 존재합니다. prototype에도 name이라는 속성이 존재합니다.  
이때 Person의 인스턴스인 boy에서 속성 name을 호출하면 'self'를 호출합니다. 물론 위처럼 `__proto__`(prototype link)를 사용하면 Parent의 속성 name을 호출할 수 있습니다.

이렇게 인스턴스 boy 안에는 자신의 속성 name과 prototype의 속성 name이 동시에 존재합니다.

여기서 Person의 직접 적용한 this.name을 삭제한 후 다시 실행하면 boy.name은 'self'가 아닌 'parent'를 호출합니다.
즉 속성 name을 호출하면 먼저 자기 자신의 속성 name을 찾고 없으면 prototype의 속성 name을 찾는 것을 알 수 있겠습니다.

Teacher는 Person을 상속받은 설계도`class`입니다. Teacher에는 속성 name을 정의하지 않았습니다. 하지만 Teacher의 인스턴스 man에서는 속성 name을 호출할 수 있습니다. 속성 name을 Teacher에서 찾고, 없으면 prototype에서 속성 name을 찾는데 prototype이 Person이라 Person의 속성 name을 찾게되는 것 입니다.
하지만 재미있게도 Person의 안에서 `this`로 선언한 속성 name은 'self'가 아니고 'parent'를 출력합니다.

여기가 제가 javascript의 객체를 공부하면서 헷갈렸던 부분입니다. 

보통(?) 객체의 설계도`class`라하면 그 객체가 설계한 모든 멤버들을 가져오는 것에 익숙했습니다.
하지만 javascript에서는 `this`는 상속에 상관없이 자기 자신에게만 적용되는 속성으로 정의되어 있습니다. 상속되는 맴버는 `prototype`으로만 정의할 수 있었습니다.


참고로 function의 name은 이렇게도 정의되어 있습니다.


```js
function Person() {
  this.name = 'self';
}

function Teacher() {
}
Teacher.prototype = Person;

var man = new Teacher();
console.log(man.name); // 'Person' 이때 'Person'은 함수 name이다. function.name 참조
```


위를 실행하면 'parent'도 아닌 'self'도 아닌 생뚱맞은 'Person'이 나왔습니다. name 속성을 찾다가 결국 찾지 못 하고, 함수 이름을 반환하는 내부 속성인 `name`을 반환했습니다.


## 마무리

javascript의 function의 특징과 다양한 사용법을 확인했습니다. 
특별한 목적을 수행하는 함수로서 function과 객체로서 function을 알 수 있었습니다. 
javascript에서는 객체 역시 유연하면서 다양한 것을 알 수 있었습니다. 
객체 안에서 this를 확인할 수 있었습니다. 
객체의 설계도를 작성하면서 햇갈렸던 부분인 prototype의 특징과 사용법을 정리했습니다. 


## 참조

> [function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions)   
> [function guide](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Functions)   
> [arrow function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)   
> [Objects](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects)   
> [function.name](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/name)
