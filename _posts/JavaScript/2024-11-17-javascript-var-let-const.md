---
title:  "[JavaScript] 변수와 상수(var, let, const)"
excerpt: "JavaScript 변수와 상수(var, let, const)"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true
 
date: 2024-11-15 23:45:30 +0900
last_modified_at: 2024-11-15 23:46:30 +0900
---

## 자바스크립트의 변수

<br>

자바스크립트에서 변수는 ```var```,```let```,```const``` 세가지 방법으로 선언할 수 있다.

```var```은 예전부터, ```let```과 ```const```는 ES6에서 새로 도입된 방법입니다.

<br>

```js
var helloVar = "Hello, World!";
console.log(helloVar);   // "Hello, World!"

let helloLet = "Hello, World!";
console.log(helloLet);   // "Hello, World!"

const helloConst = "Hello, World!";
console.log(helloConst); // "Hello, World!"
```

<br>

```var```: 같은 이름의 변수를 여러번 선언 가능, 변수 값 바꾸기 가능

```let```: 같은 이름의 변수를 여러번 선언 불가능, 변수 값 바꾸기 가능

```const```: 같은 이름의 변수를 여러번 선언 불가능, 변수 값 바꾸기 불가능

<br>

```js
var helloVar = "Hello";
var helloVar = "world";
helloVar = "hi";

let helloLet = "Hello";
let helloLet = "world";     // 오류
helloLet = "hi";

const helloConst = "Hello";
const helloConst = "world"; // 오류
helloConst = "hi";          // 오류
```