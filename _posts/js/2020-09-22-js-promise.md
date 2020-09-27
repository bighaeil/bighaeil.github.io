---
title: "Promise - js 개인 공부 정리"
categories: 
  - js
last_modified_at: 2020-09-22T20:00:00
toc: true
toc_sticky: true
---

# Promise

비동기처리를 하다보면 callback 처리를 하게 된다.  
그런데 이런 callback 처리가 많아 진다면?  

callback 으로는 이렇게 처리하게 된다.

```js
function action(i, callback) {
  setTimeout(() => {
    console.log(i);
    if (typeof callback === 'function') {
      callback(++i);
    }
  }, 1000);
}

action(0, n => {
  action(n, n => {
    action(n, n => {
      action(n, n => {
        action(n, n => {
          //end
        });
      });
    });
  });
});

```

그냥 봐도 비효율적여 보인다. 코드가 복잡한건 물론이고 보기에도 파악하기도 힘들다.

이런 상황을

`콜백 지옥 (Callback hell)`

이라 한다.

위 코드가 비현실적이라고 생각이 드는가? 무척 가능한 일이다. 비동기로 처리해야 하는 일은 상당히 많고 비중이 큰 작업도 포함되 있기 때문에 비동기로 처리되고 나서 작업해야 하는 작업들은 많을 수 밖에 없다.  

이런 비동기 작업을 편하게 처리할 수 있도록 ES6에서 추가된 것이 `Promise` 이다.  

```js
const promise = new Promise( (resolve, reject) => {
  try {
    setTimeout(() => {
      resolve('someting value');
    }, 1000);
  } catch (e) {
    reject(e);
  }
});

promise.then( res => {
  res;
}).catch( e => {
  e;
});
```

`Promise`를 생성하여 사용하는데 파라미터로 resolve와 reject를 사용한다.  

resolve는 해당 처리가 성공했을 때 전달하는 callback 이고

reject는 해당 처리가 실패했을 때 전달하는 callback 이다.  

그리고

`then`을 사용하여 resolve로 성공한 callback을 받아서 사용할 수 있고  
`catch`를 사용하여 reject로 실패한 callback을 받아서 사용할 수 있다.

아까 코드를 `promise`로 만들어보자.

```js
function action(i) {
  return new Promise( (resolve, reject) => {
    try {
      setTimeout(() => {
        console.log(i);
        resolve(++i);
      }, 1000);
    } catch(e) {
      reject(e);
    }
  });
}

action(0)
.then(i => {
  return action(i);
})
.then(action)
.then(action)
.then(action)
.catch(e => {
  console.log(e);
})
```

action 함수는 `promise`를 반환하는 함수이기 때문에 그냥 action을 넣어도 가능하다.  

`promise`를 사용하면 depth가 깊어지지 않아서 코드를 보기도 편하고 이해하기도 편하다.  

# async / await

ES6에서는 promise를 사용하는 경우 코드를 더 쉽게 만들어 주는 문법을 제공한다. 

```js
async function ready() {
  console.log('STEP1');
  await action(0);
  console.log('STEP2');
  return true;
}

ready();
```

promise를 반환하는 함수(promise 앞에)에 `await`을 붙여주고  
promise를 실행하는 함수(비동기 작업이 있는 함수)에 `async`를 붙여준다.

그러면 action 함수는 분명 비동기함수 임에도 순서대로 처리하는 것을 볼 수 있다.

promise 문법도 편하지만  
async / await 문법을 사용하면 async 함수 자체에서 분기나 로직을 작성하기가 편하게 된다.  

ready 함수는 return 값으로 Promise를 반환한다.  
그래서 ready 함수의 return 값이 true 처럼 보이지만 Promise Object 라는 것을 잊지말자.
그래서 then을 사용해서 값을 확인하자.

만약 `async`에서 에러를 잡고 싶을 때는

```js
async function go() {
  try {
    await action();
  } catch (e) {
    e;
  }
}
```

try catch 문법을 사용한다.

promise 보다 에러 처리 및 분기 처리도 편해지는 것을 볼 수 있다.

# Promise.all

작업을 하다보면 비동기처리 하나만 기다리면 좋겠지만 실재로는 그렇지 않는다.  
여러 비동기처리가 모두 실행해야 다음 처리를 해야하는 경우도 충분히 존재한다.  

이것을 생으로 구현하면 정말 콜백헬이 아닐 수 없다.  

그럴때 `Promise.all`을 사용하면 편하게 작업할 수 있다.

```js
const sleep = (ms) => {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const turtle = async () => {
  await sleep(2000);
  return 'turtle';
}

const rabbit = async () => {
  await sleep(500);
  return 'rabbit';
}

async function all() {
  return  await Promise.all([turtle(), rabbit()]);
}

all().then( res => {
  console.log(res);
})
```

코드를 보는 것과 같이 turtle()과 rabbit()은 실행해서 들어간다.  
즉 비동기처리를 실행한 결과물들을 배열로 받는 역활이다.  

`Promise.all`은 결과물들 중에 하나라도 에러가 생기면 전체 결과는 에러로 처리된다.  

# Promise.race

`Promise.all`과 비슷하지만 race는 경주라는 뜻이다. 그래서 가장 빨리 끝난 것이 `Promise.race`을 결과물이 된다.  

`Promise.race`는 가장 빨리 끝난 것이 결과물인 것 처럼 가장 나머지와 상관없이 먼저 끝난 결과물이 에러이면 에러로 처리된다.
