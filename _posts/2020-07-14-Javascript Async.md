---
layout: post
title: "Async"
description: 
headline: 
modified: 2020-07-14
category: webdevelopment
imagefeature: cover3.jpg
tags: [Async]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Callback

[비동기](https://www.youtube.com/watch?v=s1vpVCrT8f4&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=11)
[프로미스](https://www.youtube.com/watch?v=JB_yU6Oe2eE&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=12)
[async await](https://www.youtube.com/watch?v=aoQSOZfz3vQ&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=13)



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