---
title: "[JS] Node.js는 Single-thread 일까?"
excerpt: "Node.js는 Single-thread일까? Node.js의 Non-blocking, Asynchronous I/O"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true

date: 2025-02-14 20:16:00 +0900
last_modified_at: 2025-02-14 20:16:30 +0900
---

## Node.js와 Single-threaded Architecture

Node.js는 V8 JavaScript 엔진 위에서 실행되는 JavaScript 런타임 환경으로, 주로 서버 사이드 애플리케이션을 구축하는 데 사용됨.  
Node.js의 가장 큰 특징 중 하나는 single-threaded 아키텍처라는 것.

- **단일 스레드**: Node.js는 하나의 스레드에서 이벤트 루프를 통해 모든 요청을 처리.  
즉, 여러 클라이언트의 요청을 처리하는 데 여러 스레드를 사용하지 않습니다.

- **이벤트 루프**: Node.js는 이벤트 루프를 통해 비동기 I/O 작업을 관리.  
이 구조는 이벤트 기반 프로그래밍 모델을 사용하여, 비동기 작업이 완료될 때까지 기다리지 않고 다른 작업을 계속 수행할 수 있게 해줌.

- **스레드와 성능**: 단일 스레드 아키텍처는 메모리 사용량을 감소시키고, 스레드 간의 컨텍스트 스위칭 오버헤드를 줄여 성능을 향상.  
그러나 CPU 집약적인 작업(예: 이미지 처리, 비디오 인코딩 등)에서는 성능이 저하될 수 있음.  
이러한 경우에는 worker threads나 클러스터링을 사용할 수 있음.  

***Worker Threads**는 Node.js에서 제공하는 기능으로, CPU 집약적인 작업을 별도의 스레드에서 실행할 수 있게 해주는 모듈  
***클러스터링(Clustering)** 은 Node.js에서 여러 프로세스를 생성하여 다중 코어 CPU를 활용하는 방법

<br>

## Node.js의 Non-blocking, Asynchronous I/O

Node.js는 **non-blocking**과 **asynchronous I/O**를 지원하여 서버의 성능을 극대화시킴.

### Non-blocking I/O

전통적인 서버 모델에서는 I/O 작업이 완료될 때까지 기다리는 블로킹 방식이 사용되었음.  
이 방식은 리소스를 낭비하고 성능 저하를 초래할 수 있음.  

Node.js는 비동기 I/O를 통해 이러한 문제를 해결.  
I/O 작업(파일 읽기, 데이터베이스 쿼리 등)을 요청한 후, Node.js는 해당 작업이 완료될 때까지 기다리지 않고 다음 코드를 실행.  
이렇게 하면 요청 처리의 전체적인 성능을 높일 수 있음.

예를 들어, 파일을 읽는 작업을 요청하면, Node.js는 그 작업이 완료될 때까지 기다리지 않고 다른 요청을 처리함.

```js
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data); // 파일 읽기 작업이 완료되면 실행
});

console.log('이 코드는 파일 읽기 작업과 동시에 실행됩니다.');
```

<br>

### Asynchronous Callback

비동기 작업이 완료되면, 콜백 함수가 호출되어 결과를 처리.  
이 방식은 비동기 프로그래밍의 핵심으로, 코드의 흐름을 비동기적으로 처리할 수 있게 해줌.

Promise와 Async/Await: Node.js는 ES6부터 Promises와 Async/Await를 지원하여 비동기 코드를 더 간결하고 이해하기 쉽게 작성할 수 있도록 해줌

```js
const fs = require('fs').promises;

async function readFile() {
    try {
        const data = await fs.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}

readFile();
console.log('이 코드는 파일 읽기 작업과 동시에 실행됩니다.');
```


## 요약

- **Single-threaded**: Node.js는 단일 스레드 아키텍처를 사용하여 이벤트 루프를 통해 요청을 처리.  
이로 인해 메모리 사용량이 감소하고 성능이 향상됨.

- **Non-blocking, Asynchronous I/O**: Node.js는 I/O 작업을 비동기적으로 처리하여 높은 동시성을 유지.  
비동기 작업이 완료되면 콜백 함수가 호출되며, Promises와 Async/Await를 통해 비동기 코드를 더 쉽게 작성할 수 있음.