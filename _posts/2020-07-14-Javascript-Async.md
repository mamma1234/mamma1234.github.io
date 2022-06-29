---
layout: post
title: 'JavaScript Async'
description:
headline:
modified: 2020-07-14
category: webdevelopment
imagefeature:
tags: [JavaScript Async]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# 비동기 프로세스

-   동영상

-   [비동기] (https://www.youtube.com/watch?v=s1vpVCrT8f4&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=11)
-   [프로미스] (https://www.youtube.com/watch?v=JB_yU6Oe2eE&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=12)
-   [async await] (https://www.youtube.com/watch?v=aoQSOZfz3vQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=13)

## 목차

-   [Callback](#Callback)
-   [Promise](#Promise)
-   [Async](#Async)
-   [Async & Await](#Async-&-Await)
    -   [Callback -> Async](#Callback-->-Async)
-   [await Promise.all](#await-Promise.all)
-   [async function 표현식](#async-function-표현식)

# Callback

```JavaScript
//Synchronous callback
function printImmediately(print) {
    print();
}
printImmediately(() => console.log("hello"));

//Asynchronous callback
function printWithDelay(print, timeout) {
    setTimeout(print, timeout);
}
printWithDelay(() => console.log("async callck"), 2000);
```

```JavaScript
// 콜백, callback function using funtion expression
function callbackTest(data, printYes, printNo) {
  if (data === "yes") {
    printYes();
  } else {
    printNo();
  }
}

const printYes = function() {
  console.log("yes");
};

const printNo = function() {
  console.log("no");
};

callbackTest("yes", printYes, printNo);
callbackTest("No", printYes, printNo);
```

```JavaScript
// 콜백 지옥, Callback Hell example
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    setTimeout(() => {
      if (
        (id === "ellie" && password === "dream") ||
        (id === "coder" && password === "academy")
      ) {
        onSuccess(id);
      } else {
        onError(new Error("not found"));
      }
    }, 2000);
  }

  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === "ellie") {
        onSuccess({ name: "ellie", role: "admin" });
      } else {
        onError(new Error("no access"));
      }
    }, 1000);
  }
}

const userStorage = new UserStorage();
// const id = prompt("enter your id");
// const password = prompt("enter your password");
const id = "ellie";
const password = "dream";
userStorage.loginUser(
  id,
  password,
  user => {
    userStorage.getRoles(
      user,
      userWithRole => {
        alert(
          `Hello ${userWithRole.name}, you have a ${userWithRole.role} role`
        );
      },
      error => {
        console.log("1.", error);
      }
    );
  },
  error => {
    console.log("2.", error);
  }
);

```

# Promise

-   Promise 는 3가지 상태가 존재한다.
    -   Pending(대기, 비동기 처리 로직이 아직 완료되지 않은 상태) : new Promise() 메서드를 호출하면 Pending 상태가 된다. 이 때 콜백함수를 선언할 수 있다.
    -   Fulfilled(이행, 비동기 처리가 완료되어 프로미스가 결과 값을 반환해 준 상태) : 콜백 함수에서 resolve를 실행하는 경우로 resolve 상태가 되면 then()을 이용해 처리 결과 값을 받을 수 있다.
    -   Rejected(실패, 비동기 처리가 실패하거나 오류가 발생한 상태) : 콜백 함수에서 reject를 실행하는 경우로 reject 상태가되면 catch()를 통해 실패 처리 값을 받을 수 있다.

```JavaScript
// pending 대기상태
var pending = new Promise((resolve) => {});
console.log(pending);
// pending
// [[PromiseStatus]]: "pending"
// [[PromiseValue]]: undefined

// fulfilled 성공상태
var fulfilled = new Promise((resolve) => resolve('fulfilled'))
console.log(fulfilled);
// resolved
// [[PromiseStatus]]: "resolved"
// [[PromiseValue]]: "fulfilled"

// rejected 실패상태
var rejected = new Promise((resolve, reject) => {
    throw new Error('rejected');
    reject();
});
console.log(rejected);
// rejected
// [[PromiseStatus]]: "rejected"
// [[PromiseValue]]: Error: rejected at <anonymous>

var catchError = new Promise((resolve, reject) => {
    throw new Error('rejected')
}).catch(() => { return 'catchValue' })
console.log(catchError);
// pending
// [[PromiseStatus]]: "resolved"
// [[PromiseValue]]: "catchValue"

var catchThen = new Promise((resolve, reject) => {
    reject('rejected')
}).then(null, (error) => { return 'catchThen' }
).catch(() => { return 'catchValue' });
console.log(catchThen);
// pending
// [[PromiseStatus]]: "resolved"
// [[PromiseValue]]: "catchThen"
```

```JavaScript
// promise is a JavaScript object for asynchronous operation.
// state: pending -> fulfilled or rejected
// Producer vs Consumer

// 1.Producer
// Promise(executor: (resolve: (value?: any) => void, reject: (reason?: any) => void) => void):
// when new Promise is created, the executor runs automatically.
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("ellie");
    //reject(new Error("no network"));
  }, 2000);
});

// 2. Consumers: then , catch, finally
promise
  .then(value => {
    console.log(value);
  })
  .catch(error => {
    console.log(error);
  })
  .finally(() => console.log("finally"));

// 3. Promise chaining
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(1);
  }, 1000);
});

fetchNumber
  .then(num => num * 2)
  .then(num => num * 3)
  .then(num => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000);
    });
  })
  .then(num => console.log(num));



// 4. Error Handling
const getHen = () =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`chick`), 1000);
  });

const getEgg = hen =>
  new Promise((resolve, reject) => {
    // setTimeout(() => resolve(`${hen} -> egg`), 1000);
    setTimeout(() => reject(new Error(`error! ${hen} -> egg`)), 1000);
  });

const cook = egg =>
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} -> eat`), 1000);
  });

// getHen()
//   .then(hen => getEgg(hen))
//   .then(egg => cook(egg))
//   .then(meal => console.log(meal));

// getHen()
//   .then(getEgg)
//   .then(cook)
//   .then(console.log);

getHen()
  .then(getEgg)
  .catch(error => {
    return "bread";
  })
  .then(cook)
  .then(console.log)
  .catch(console.log);

```

## Callback -> Promise

```JavaScript
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (
          (id === "ellie" && password === "dream") ||
          (id === "coder" && password === "academy")
        ) {
          resolve(id);
        } else {
          reject(new Error("not found"));
        }
      }, 2000);
    });
  }

  getRoles(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === "ellie") {
          resolve({ name: "ellie", role: "admin" });
        } else {
          reject(new Error("no access"));
        }
      }, 1000);
    });
  }
}

const userStorage = new UserStorage();
const id = "ellie";
const password = "dream";

userStorage
  .loginUser(id, password)
  .then(userStorage.getRoles)
  .then(user =>
    console.log(`2. Hello ${user.name}, you have a ${user.role} role`)
  )
  .catch(console.log);

```

# Async

-   async function 선언은 AsyncFunction객체를 반환하는 하나의 비동기 함수를 정의합니다. 비동기 함수는 이벤트 루프를 통해 비동기적으로 작동하는 함수로, 암시적으로 Promise를 사용하여 결과를 반환합니다. 그러나 비동기 함수를 사용하는 코드의 구문과 구조는, 표준 동기 함수를 사용하는것과 많이 비슷합니다.

-   async 함수는 항상 promise를 반환합니다. 만약 async 함수의 반환값이 명시적으로 promise가 아니라면 암묵적으로 promise로 감싸집니다.

```JavaScript
예를 들어

async function foo() {
    return 1
}
위 코드는 아래와 같습니다.

function foo() {
    return Promise.resolve(1)
}
```

-   실제로는 fulfil Promise가 반환되기 때문에 반환된 값을 사용하기 위해선 .then() 블럭을 사용해야 합니다.

```JavaScript
hello().then((value) => console.log(value))

짧게 표현하면 아래와 같이 쓸 수 있습니다.

hello().then(console.log)
```

-   async 함수의 본문은 0개 이상의 await 문으로 분할된 것으로 생각할 수 있습니다. 첫번째 await 문을 포함하는 최상위 코드는 동기적으로 실행됩니다. 따라서 await 문이 없는 async 함수는 동기적으로 실행됩니다. 하지만 await 문이 있다면 async 함수는 항상 비동기적으로 완료됩니다.

```JavaScript
예를 들어

async function foo() {
    await 1
}
위 코드는 아래와 같습니다.

function foo() {
    return Promise.resolve(1).then(() => undefined)
}
```

# Async & Await

```JavaScript
// async & await
// clear style of using promise :)
// 1. async
async function fetchUser() {
  // do network request in 10 secs..
  return "ellie1";
}

const user = fetchUser();
user.then(console.log);
console.log(user);

// 2. await
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
  await delay(3000);
  return "apple";
}

async function getBanana() {
  await delay(3000);
  return "banana";
}

//chaining 지옥
function pickFruits() {
  return getApple().then(apple => {
    return getBanana().then(banana => `1.${apple}+${banana}`);
  });
}

//async 로 개선 - 직렬 처리
async function pickFruits2() {
  const apple = await getApple();
  const banana = await getBanana();
  return `2.${apple}+${banana}`;
}

//async 로 개선 - 병렬 처리
async function pickFruits3() {
  const applePromise = getApple();
  const bananaPromise = getBanana();
  const apple = await applePromise;
  const banana = await bananaPromise;
  return `3.${apple}+${banana}`;
}

pickFruits().then(console.log);
pickFruits2().then(console.log);
pickFruits3().then(console.log);

// 3. useful Promise APIs
function pickAllFruits() {
  return Promise.all([getApple(), getBanana()]).then(fruits =>
    fruits.join(" (+) ")
  );
}
pickAllFruits().then(console.log);

function pickOnlyOne() {
  return Promise.race([getApple(), getBanana()]);
}

pickOnlyOne().then(console.log);
```

## Callback -> Async

```JavaScript
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (
          (id === "ellie" && password === "dream") ||
          (id === "coder" && password === "academy")
        ) {
          resolve(id);
        } else {
          reject(new Error("not found"));
        }
      }, 2000);
    });
  }

  getRoles(user) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        if (user === "ellie") {
          resolve({ name: "ellie", role: "admin" });
        } else {
          reject(new Error("no access"));
        }
      }, 1000);
    });
  }

  // 이거 추가함
  async getUserWithRole(user1, password1) {
    const user2 = await this.loginUser(user1, password1);
    const role = await this.getRoles(user2);
    return role;
  }
}

const userStorage = new UserStorage();
const id = "ellie";
const password = "dream";

// userStorage
//   .loginUser(id, password)
//   .then(userStorage.getRoles)
//   .then(user =>
//     console.log(`2. Hello ${user.name}, you have a ${user.role} role`)
//   )
//   .catch(console.log);

userStorage
  .getUserWithRole(id, password) //
  .catch(console.log)
  .then(console.log);


```

# await Promise.all

-   await 을 사용하여 세 가지 Promise의 결과가 반환되었을 때 values 배열에 담을 수 있습니다

```JavaScript
async function fetchAndDecode(url, type) {
  let response = await fetch(url);

  let content;

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  } else {
    if(type === 'blob') {
      content = await response.blob();
    } else if(type === 'text') {
      content = await response.text();
    }
  }

  return content;


}

async function displayContent() {
  let coffee = fetchAndDecode('coffee.jpg', 'blob');
  let tea = fetchAndDecode('tea.jpg', 'blob');
  let description = fetchAndDecode('description.txt', 'text');

  let values = await Promise.all([coffee, tea, description]);

  let objectURL1 = URL.createObjectURL(values[0]);
  let objectURL2 = URL.createObjectURL(values[1]);
  let descText = values[2];

  let image1 = document.createElement('img');
  let image2 = document.createElement('img');
  image1.src = objectURL1;
  image2.src = objectURL2;
  document.body.appendChild(image1);
  document.body.appendChild(image2);

  let para = document.createElement('p');
  para.textContent = descText;
  document.body.appendChild(para);
}

displayContent()
.catch((e) =>
  console.log(e)
);
```

# async function 표현식

-   문법

    -   async function [name]([param1[, param2[, ..., paramN]]]) { statements }

-   인수

    -   name
        -   함수 이름. 생략가능하며 이경우함수는 anonymous 형식임 이름은 함수 몸체에 대해 지역적으로 사용.
    -   paramN
        -   함수에 전달될 인수의 이름.
    -   statements
        -   함수 몸체를 구성하는 명령문들.

-   Simple example

```JavaScript
function resolveAfter2Seconds(x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
};


var add = async function(x) { // async function 표현식을 변수에 할당
  var a = await resolveAfter2Seconds(20);
  var b = await resolveAfter2Seconds(30);
  return x + a + b;
};

add(10).then(v => {
  console.log(v);  // 4초 뒤에 60 출력
});


(async function(x) { // async function 표현식을 IIFE로 (즉시실행 함수(Immediately Invoked Function Expression)) 사용
  var p_a = resolveAfter2Seconds(20);
  var p_b = resolveAfter2Seconds(30);
  return x + await p_a + await p_b;
})(10).then(v => {
  console.log(v);  // 2초 뒤에 60 출력
});

```
