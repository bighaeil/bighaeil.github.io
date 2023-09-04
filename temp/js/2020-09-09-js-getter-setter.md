---
title: "getter 와 setter - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-09T20:30:00
toc: true
toc_sticky: true
---

# getter 와 setter - ES6

`getter` 특정값을 조회한다.

`setter` 특정 값을 입력한다.


## getter

```js
const move = {
  x: 1,
  y: 2,
  get position() {
    return `(${this.x}, ${this.y})`;
  }
}

move.position; // (1, 2)
```

`positon` 은 함수처럼 보이는데 `move.positon()` 이렇게 사용하지 않았다.

`get` 키워드를 붙여서 함수처럼 호출하지 않아도  

해당 값(postion)을 조회할 수 있다.


## setter

```js
const move = {
  x: 1,
  y: 2,
  get position() {
    return `(${this.x}, ${this.y})`;
  },
  set goX(value) {
    this.x = value;
  }
}

move.goX = 2;
move.positon; // (2, 2)
```

`set` 키워드를 사용하여 move 객체의 x 값을 수정할 수 있다.

역시 함수처럼 호출하지 않고 객체의 속성처럼 호출 할 수 있다.


## 객체의 정보은닉

```js
const obj = {
  _a: 1,
  _b: 2,
  get a() {
    return this._a;
  },
  get b() {
    return this._b;
  },
  set a(value) {
    this._a = value;
  },
  set b(value) {
    this._b = value;
  }
}
```

객체 `obj` 는 분명 _a, _b 를 가지고 있지만 외부에서 `obj` 를 사용할 때는  
`a`, `b` 로 접근해야 한다.  

이는 객체의 `정보은닉`으로 자신의 정보를 숨기고 자신의 연산만을 통해서 접근을 허용한다.  


## getter와 setter 활용

```js
const obj = {
  _a: 1,
  _b: 2,
  _sum: 3,
  get a() {
    return this._a;
  },
  get b() {
    return this._b;
  },
  get sum() {
    return this._sum;
  },
  set a(value) {
    this._a = value;
    this._sum = this._a + this._b;
  },
  set b(value) {
    this._b = value;
    this._sum = this._a + this._b;
  }
}
```

```js
const obj2 = {
  a: 1,
  b: 2,
  sum: function() {
    return a + b;
  }
}
```

`obj` 와 `obj2` 의 차이점은 obj 는 sum 을 호출할 때 연산을 하지 않고 obj2 는 sum 을 호출할 때마다 연삭을 한다는 점.

뭐가더 좋을지는 알아서 판단
