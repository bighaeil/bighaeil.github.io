---
title: "JAVASCRIPT STUDY ARRAY"
categories:
    - study
last_modified_at: 2021-12-05T12:35:00
toc: true
toc_sticky: true
---

# ARRAY

자바스크립트에서 사용하는 ARRAY관련 특성과 함수를 정리해보았습니다.
개인적으로 중요하다고 생각하는 부분만 추린 것으로 알아두면 개발에 유용할 것이라고 생각합니다.
ES5 기준으로 작성하고 ES6를 설명하는 경우는 따로 명시하겠습니다.


## 기본

```js
var arr1 = [];
var arr2 = new Array();
var arr3 = [1, '0', {}];
var arr4 = [];
arr4[4] = 4;
arr4[99] = 99;
```

자바스크립트에서 배열은 보통 arr1으로 작성합니다. 물론 arr2로도 작성이 가능하고 동작은 arr1과 다르지 않습니다.
모든 배열은 Array.prototype을 상속하기 때문에 Array에 새로운 메서드나 속성을 추가하고 싶다면 Array를 사용할 수 있겠습니다.

배열은 arr3처럼 생성과 동시에 초기값을 넣으 수 있습니다.
arr3처럼 다양한 타입의 요소를 넣을 수 있지만 좋은 코드가 아니기 때문에 사용하지 않습니다.

배열은 arr4처럼 생성하고 배열 크기를 정하지 않아도 마음대로 값을 할당할 수 있습니다. 하지만 역시 좋은 코드가 아니기 때문에 사용하지 않습니다.

유연한 배열은 쉽게 코드를 작성할 수 있지만 일관성이 없어지고 예측할 수 없게되어 코드를 어지럽게 만들기 때문에 정해진 방법안에서 사용하기 바랍니다.


## for

`for` 문은 괄호`()`로 감싸고 세미콜론`;`으로 구분한 세 개의 선택식과 반복을 수행할 블럭문`{}`으로 이루어져 있습니다.

```js
for (var i=0; i < arr.length ;i++) {
    //
}
```

다음과 같은 for 문도 존재합니다.


### for ... in

객체가 열거형 속성을 반복하여 조회합니다.

```js
for (var property in object) {
    console.log(arr[property]);
}
```

이때 property는 object의 열거형 속성입니다. 이 속성을 사용해 값을 가져오기 위해서는

`arr[property]`

이렇게 작성할 수 있습니다. 배열과 비슷하다고 배열과 혼동해서는 안되겠습니다. 위에서 설명한 것 처럼 객체의 열거형 속성을 조회합니다.


### 열거형 속성(Enumerable properties)

객체 내부에 열거형 플래그가 true로 설정된 property로 간단하게 표현해보면 

```js
var obj = {
    a: 1
};
obj.b = 2;
Object.defineProperty(obj, 'c', {
    value: 3,
    writable: true,
    enumerable: true,
    configurable: true
});
```

객체의 속성을 단순히 생성하거나 defineProperty을 사용하여 enumerable이 true로 설정하여 속성의 성격을 결정할 수 있습니다.

!Array에서는 사용할 수 없습니다.

### for ... of

반복가능한 객체(Iteration protocols)를 반복하고 각 속성값을 조회합니다. ES6에서 가능합니다.

```js
for (const element of arr) {
    console.log(element);
}
```


### 반복가능한 객체(Iteration protocols)

예를들면 Array, Map, Set, String, arguments, rest arguemnts 처럼 반복가능한 객체를 말합니다.


### 주의

!여기서 주목할 점은 반복문을 수행하는 영역이 블럭문이라는 것입니다.

javasrcipt는 `var`로 선언한 변수는 scope가 함수 범위를 가집니다. 즉 블럭 범위를 가지지 않습니다. 그래서 for 문안에서 선언한 변수는 블록문 바깥까지 영향을 미칩니다. 이는 예기치 못한 동작을 수행합니다.

```js
var x = 1;
{
    var x = 2;
}
x; // output: 2
```

`var`를 사용할 때는 이를 염두하고 프로그램을 작성해야합니다. 하지만 그럼에도 실수할 수 있는 변수입니다. 그러므로

> `var` 변수는 사용하지 마세요.


---

개인적으로 for문은 배열의 모든 요소를 수행할 필요가 없을때 말고는 잘 사용하지 않습니다.
왜냐면 for문으로는 현재 반복문이 어떤 역활을 수행하는지 알려주지 않기 때문입니다.
반면에 배열 내부에는 반복문을 도와주는 유용한 메소드가 많이 존재합니다.
메서드는 사용하기 편리한 것 뿐만아니라 어떤 목적에서 반복문을 수행하고 있는지 명확하게 알려주기 때문에 적극적으로 사용하는 것을 추천합니다.


## 메서드

배열의 메서드에는 여러가지가 있지만 개인적으로 다음과 같은 특성이 있는지 확인하고 사용합니다.

1. 결과값으로 새로운 배열이 생성하는가
2. 기존 배열에 영향을 주는가

위 특성을 확인하면서 자주 사용하는 메서드들을 확인해보자.

### push()

배열의 끝에 하나 이상의 요소를 추가합니다. 즉 기존 배열에 크기가 증가합니다.

```js
arr.push('a', 'b', 'c')
```

|---||
|매개변수|배열 끝에 추가할 요소, 콤마`,`로 구분|
|반환 값|배열의 최종 length|

### pop()

배열의 마지막 요소를 제거하고 그 요소를 반환합니다. 즉 기존 배열의 크기가 하나 감소합니다.

```js
var item = arr.pop()
```

|---||
|매개변수||
|반환 값|배열이 있으면 배열의 마지막 요소, 없으면 `undefined`|


### sort()

배열의 요소를 정렬합니다. 기본 정렬 순서는 문자열의 유니코드를 따릅니다. 즉 문자열의 오름차순으로 정렬됩니다.

```js
const arr = [1, 30, 4, 21, 100000];
arr.sort(); // output: [1, 100000, 21, 30, 4]
```

위 처럼 요소를 문자열로바꿔서 정렬하거나 정직하게 순수데이터로 정렬하는 경우는 거의 없었고 값이나 객체를 정렬하는 경우가 많았기 때문에 아래처럼 사용합니다.

```js
var arr = [{n: 3}, {n: 2}, {n: 1}];
arr.sort(function (a, b) {
    if (a.n < b.n) {
        return -1;
    }
    if (a.n > b.n) {
        return 1;
    }
    return 0;
});
```

callback 함수를 이용하여 a와 b를 비교하여 작으면 a가 작으면 -1을 반환, a가 크면 1을 반환, 같으면 0을 반환하도록 만들어 사용합니다.

sort 함수는 원본 배열을 변환하기 때문에 주의해서 사용해야합니다. 반환값 역시 정렬된 원본 배열 입니다.


### splice()

배열의 기존 요소를 삭제 또는 교체하거나 새로운 요소를 추가하여 배열의 내용을 변경합니다. 즉 원본 배열을 변경됩니다.

```js
var arr = ['a', 'b', 'e', 'd'];
arr.splice(2, 1, 'c'); // output: [1, 2, 3, 4]
```

> arr.splice(start, deleteCount, items)

|매개변수|설명|optional|
|---|---|---|
|start|배열의 변경을 시작할 인덱스 입니다. 0부터 시작합니다. -1은 -n과 값습니다. 즉 요소의 끝을 가리키며 `arr.length - n`과 같습니다.||
|deleteCount|삭제할 요소의 수입니다. 생략하면 모든 요소를 제거합니다.||
|items|배열에 추가할 요소입니다. 콤마`,`로 구분합니다.||

splice 매서드는 원본 배열을 변경합니다. 반환 값으로 제거한 요소들을 담은 배열을 반환합니다.


### concat()

두 배열을 합쳐서 새로운 배열을 반환합니다. 기존 배열은 변경하지 않습니다.

```js
var arr1 = [1, 2, 3];
var arr2 = [4, 5, 6];
var arr = arr1.concat(arr2); // output: [1, 2, 3, 4, 5, 6]
```

concat은 배열의 얕은 복사에도 사용합니다. 배열을 복사하긴 하지만 요소가 객체인 겨우 참조만 하기 때문에 사용시 유의해야 합니다.


### filter()

테스트를 통과한 모든 요소를 모아 새로운 배열을 반환합니다.

```js
var arr = [1, 2, 3, 4, 5];
var result = arr.filter(function (item) {
    return item < 4;
}); // output: [1, 2, 3]
```

> arr.filter(callback(element[, index[, array]])[, thisArg])

|매개변수|설명|optional|
|---|---|---|
|callback|각 요소를 테스트하는 함수. true를 반환하면 요소를 유지하고, false 를 반환하면 요소를 버립니다.||
|element|처리할 현재 요소||
|index|처리하는 요소의 인덱스|true|
|array|원본 배열|true|
|thisArg|callback을 실행할 때 this로 사용하는 값|true|


### join()

배열의 모든 요소를 연결해 하나의 문자열로 만듭니다.

```js
var arr = ['a', 'b', 'c'];
arr.join(); // output: 'a,b,c'
arr.join(''); // output: 'abc'
arr.join('-'); // output: 'a-b-c'
```

|---||
|매개변수|separator를 요소 사이를 채웁니다. separator가 없는 경우 콤마`,`로 채웁니다.|
|반환 값|separator를 포함한 문자열|


### slice()

배열의 일부를 추출하여 얕은 복사의 새로운 배열을 반환합니다. 원본 배열은 바뀌지 않습니다.

```js
var arr = [1, 2, 3, 4, 5] ;
var result = arr.slice(2, 4); // output: [3, 4]
```

> arr.slice([begin, [, end]])

|매개변수|설명|optional|
|---|---|---|
|begin|추출하는 시점의 인덱스. begin을 포함합니다. 만약 begin이 없으면 0번 index 부터 slice 합니다.|true|
|end|추출을 종료하는 인덱스. end는 포함하지 않습니다. 음수일 경우 배열의 끝에서부터의 인덱스를 나타냅니다.|true|

반환값이 추출한 새로운 배열입니다.

splice와 다른점은 splice 는 원본 배열에 영향을 주지만 slice는 원본 배열은 바뀌지 않기 때문에 개인적으로 splice보다 slice를 선호합니다.

splice는 주로 요소를 특정위치에 삽입할때 주로 사용합니다.


### find()

주어진 조건을 만족하는 첫 번째 요소를 반환합니다. 없으면 `undefined`를 반환합니다. ES6 문법이라 주의가 필요합니다.

```js
const arr = [1,2,3,4,5];
const result = arr.find(item => item > 1); // output: 2
```


### forEach()

배열을 순회하면서 callback을 수행합니다.

```js
arr.forEach(function (item) {
    console.log(item);
});
```

> arr.forEach(callback(element[, index[, array]])[, thisArg])

|매개변수|설명|optional|
|---|---|---|
|callback|각 요소를 처리하는 함수||
|element|처리할 현재 요소||
|index|처리하는 요소의 인덱스|true|
|array|원본 배열|true|
|thisArg|callback을 실행할 때 this로 사용하는 값|true|

forEach는 단지 배열을 순회할뿐 어떤 값을 반환하지 않습니다.


### map()

배열 내의 모든 요소에 대하여 처리한 결과를 모아 새로운 배열로 반환합니다.

```js
const arr = [1, 2, 3];
const result = arr.map(x => x * x); // output: [1, 4, 9]
```

> arr.map(callback(element[, index[, array]])[, thisArg])

|매개변수|설명|optional|
|---|---|---|
|callback|각 요소를 처리하는 함수. 결과를 모아서 새로운 배열을 반환합니다.||
|element|처리할 현재 요소||
|index|처리하는 요소의 인덱스|true|
|array|원본 배열|true|
|thisArg|callback을 실행할 때 this로 사용하는 값|true|

모든 요소를 처리하는 점을 염두해야합니다. 즉 falsy를 반환한다고 해서 스킵하지 않습니다.


### reduce()

각 요소에 주어진 리듀서(reducer) 함수를 실행하고 하나의 결과값을 반환합니다.

```js
var arr = [1, 2, 3];
var reducer = function (accumulator, currentValue) {
    return accumulator + currentValue;
}
// 1 + 2 + 3
var result1 = arr.reduce(reducer); // output: 6
// 5 + 1 + 2 + 3
var result2 = arr.reduce(reducer, 5); // output: 11
```

> callback(accumulator, currentValue, currentIndex, array)
> arr.reduce(callback[, initialValue])


|매개변수|설명|optional|
|---|---|---|
|callback|각 요소를 처리하는 함수.||
|accumulator|누산기. callback의 반환값을 누적합니다. callback의 첫 호출시 initialValue가 존재하면 accumulator의 초기값은 initialValue이 되고 initialValue가 존재하지 않으면 accumulator의 초기값은 배열의 첫 번째 요소입니다.||
|currentValue|처리할 현재 요소||
|currentIndex|처리할 현재 요소의 인덱스. 첫 호출시 initialValue가 존재하면 0, 아니면 1부터 시작합니다.|true|
|array|원본 배열|true|
|initialValue|callback의 최초 호출시 제공하는 값.|true|

만약 빈 배열에 reduce를 수행하는데 initialValue가 없으면 `error`를 호출합니다. 어찌보면 당연한게 currentValue에서 arr[1]가 존재하지 않기 때문입니다.


### some()

배열 안의 어떤 요소라도 테스트를 통과하면 true 아니면 false를 반환합니다.

```js
const arr = [1, 2, 3];
const even = arr.some((element) => element % 2 === 0); // output: true
```

ES6에서 사용가능합니다.

### every()

배열 안의 모든 요소가 테스트를 통과하면 true 아니면 false를 반환합니다.

```js
const arr = [1, 2, 3];
const result = arr.some((element) => element < 5); // output: true
```

ES6에서 사용가능합니다.


## 전개 구문(spread syntax)

배열 혹은 객체 등 반복가능한 객체를 키와 값으로 확장시킬 수 있습니다.

!spread는 기존 객체로 새로운 객체를 생성하지만 얕은 복사라는 점을 유의합니다.

### 함수 호출에서 spread

```js
const sum = (x, y, z) => x + y +z;
const arr = [1, 2, 3];
sum(...arr); // output: 6
```


### 배열에서 spread

배열의 요소들을 이미 존재하는 배열의 일부로 하는 새로운 배열을 생성할 수 있습니다.

```js
const arr = [3, 4, 5];
const newArr= [1, 2, ...arr, 6, 7]; // output: [1, 2, 3, 4, 5, 6, 7]
```


### 객체에서 spread

객체의 열거형 속성을 전개하여 다른 객체의 속성으로 하는 새로운 객체를 생성할 수 있습니다.

```js
const obj = {a: 1, b: 2, c: 3};
const newObj = {...obj, c: 4}; // output: {a: 1, b: 2, c: 4}
```

spread는 중복되는 속성의 경우 나중에 열거된 속성으로 결정된다는 점을 유의합니다.


## 참조
> [Array](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)   
> [Enumerable properties](https://developer.mozilla.org/ko/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)   
> [defineProperty](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)   
> [Iteration protocols](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Iteration_protocols)   
> [rest parameters](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)   
