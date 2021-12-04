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

ES5 기준으로 작성하고 ES6 문법은 정리하지 안았습니다.

기본적일 수도 있지만 개인적으로 중요하다고 생각하는 부분만 추린 것으로

알아두면 실제 개발에 유용할 것이라고 생각합니다.

## 기본

```ja
var arr1 = [];
var arr2 = new Array();
var arr3 = [1, '0', {}];
var arr4 = [];
arr4[4] = 4;
arr4[99] = 99;
```

자바스크립트에서 배열은 보통 arr1으로 작성합니다. 물론 arr2로도 작성이 가능하고 동작은 arr1과 다르지 않습니다.
다만 모든 배열은 Array.prototype을 상속하기 때문에 Array에 새로운 메서드나 속성을 추가하고 싶다면 Array를 사용할 수 있겠습니다.

