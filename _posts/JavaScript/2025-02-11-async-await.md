---
title: "[JS] async와 await"
excerpt: "JavaScript의 비동기 프로그래밍을 더욱 간단하고 가독성 있게 만들어 주는 기능인 async와 await 알아보기"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true

date: 2025-02-11 21:18:30 +0900
last_modified_at: 2025-02-11 21:19:30 +0900
---

## async/await란?

JavaScript에서 `async/await`는 비동기 코드를 동기처럼 작성할 수 있게 해주는 문법  
이는 Promise를 기반으로 하며, 비동기 작업을 더 간결하고 읽기 쉽게 만들어 줌  
`async/await`를 사용하면 콜백 지옥을 피하고, 복잡한 비동기 로직을 간단하게 표현할 수 있음

<br>

### async

`async`는 함수를 비동기 함수로 정의  
이 함수는 항상 Promise를 반환  
만약 함수 내에서 다른 값을 반환하면, JavaScript는 자동으로 해당 값을 `Promise.resolve()`로 감싸서 반환

```js
async function myAsyncFunction() {
    return "이 값은 Promise로 감싸집니다.";
}

myAsyncFunction().then(result => {
    console.log(result); // "이 값은 Promise로 감싸집니다."
});
```

```js
async function myAsyncFunction() {
    return Promise.resolve("이 값은 Promise로 감싸집니다.");
}

myAsyncFunction().then(result => {
    console.log(result); // "이 값은 Promise로 감싸집니다."
});
```

1번과 2번 코드는 동일한 동작을 함

<br>

### await

`await`는 내부적으로 `Promise.then()`을 사용  
await는 Promise가 이행(fulfilled)될 때까지 기다린 후, 그 결과 값을 반환

```js
async function fetchData() {
    const result = await Promise.resolve("Data Loaded");
    console.log(result); // Data Loaded
}
fetchData();
```

내부적으로는 이렇게 동작

```js
function fetchData() {
    return Promise.resolve("Data Loaded").then(result => {
        console.log(result);
    });
}
fetchData();
```

await는 내부적으로 Promise.then()을 사용하여 동작하며, 해당 Promise가 완료될 때까지 기다린 후 결과 값을 반환하는 것과 같음

<br>

### 에러 처리

`async/await`를 사용할 때는 `try/catch` 블록을 사용하여 에러를 처리할 수 있음 
이는 비동기 작업에서 발생할 수 있는 오류를 관리하는 데 유용

```js
async function fetchDataWithErrorHandling() {
    try {
        const response = await fetch("https://api.example.com/data");
        if (!response.ok) {
            throw new Error("네트워크 응답이 좋지 않습니다.");
        }
        const data = await response.json();
        return data;
    } catch (error) {
        console.error("데이터를 가져오는 중 오류 발생:", error);
    }
}

fetchDataWithErrorHandling();
```