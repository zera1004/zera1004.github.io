---
title: "[JS] var, let, const란?"
excerpt: "JavaScript의 변수 선언 방법인 var, let, const의 차이점과 사용법 알아보기"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true

date: 2025-02-10 20:48:30 +0900
last_modified_at: 2025-02-10 20:49:30 +0900
---

## var 변수 선언

`var`는 JavaScript가 처음 등장할 때부터 사용된 변수 선언 방식

- **함수 스코프(Function Scope)**  
   `var`로 선언한 변수는 해당 변수가 속한 함수 내에서만 유효함  
   함수 외부에서 선언된 경우 전역(global) 변수가 됨

  ```js
  function exampleFunction() {
    if (true) {
      var x = 10; // x는 if문 블록 내에서 선언했지만,
    }
    console.log(x); // 함수 전체에서 접근 가능 → 출력: 10
  }
  ```

- **재선언 가능**  
  같은 스코프 내에서 `var`로 동일한 변수명을 여러 번 선언할 수 있음

  ```js
  var x = 10;
  var x = 20;
  console.log(x); // 20
  ```

- **재할당 가능**  
  `var`로 선언한 변수는 재할당 가능

  ```js
  var x = 10;
  x = 20;
  console.log(x); // 20
  ```

- **호이스팅(Hoisting)**  
  변수 선언이 해당 스코프의 최상단으로 끌어올려지는 현상이 발생  
  단, 할당은 호이스팅되지 않으므로, 초기화 전에 변수를 사용하면 `undefined`가 됨

  ```js
  console.log(x); // undefined (호이스팅으로 인해 선언은 되었지만 초기화 전)
  var x = 10;
  ```

**\*호이스팅: 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당 하는 것**

<br>

## let 변수 선언

ES6(ECMAScript 2015)부터 도입된 `let`은 `var`의 단점을 보완하기 위해 만들어짐

- **블록 스코프(Block Scope)**  
  중괄호 {}로 감싼 코드 블록 내에서만 유효  
  이는 반복문, 조건문 등에서 의도치 않은 변수 충돌을 막아줌

  ```js
  function exampleFunction() {
    if (true) {
      let x = 10; // x를 if문 내에서 선언
    }
    console.log(x); // ReferenceError: x is not defined
  }
  ```

- **재선언 불가**  
  같은 스코프 내에서 `let`으로 이미 선언된 변수는 다시 선언할 수 없음

  ```js
  let x = 10;
  let x = 20; // SyntaxError: Identifier 'x' has already been declared
  ```

- **재할당 가능**
  `let`으로 선언한 변수는 재할당 가능

  ```js
  let x = 10;
  x = 20;
  console.log(x); // 20
  ```

- **호이스팅**  
  `let`도 호이스팅되지만, **"일시적 사각지대(Temporal Dead Zone, TDZ)"** 가 발생하여 선언 전에 접근하면 에러가 발생

  ```js
  console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 10;
  ```

<br>

## const 변수 선언

`const` 역시 ES6에서 도입되었으며, **상수(Constant)** 를 선언할 때 사용

- **블록 스코프(Block Scope)**
  `let`과 마찬가지로 코드 블록 내에서만 유효

  ```js
  if (true) {
    const x = 50;
    console.log(x); // 출력: 50
  }
  console.log(x); // ReferenceError: x is not defined
  ```

- **재선언 및 할당 불가**
  `const`로 선언한 변수는 재선언과 재할당이 불가능

  ```js
  const x = 100;
  const x = 200; // SyntaxError: Identifier 'x' has already been declared
  ```

  ```js
  const x = 100;
  x = 150; // TypeError: Assignment to constant variable.
  ```

- **호이스팅**  
  `const`도 `let`과 마찬가지로 호이스팅되지만, **"일시적 사각지대(Temporal Dead Zone, TDZ)"** 가 발생하여 선언 전에 접근하면 에러가 발생

- **불변 객체?**
  `const`로 선언한 객체나 배열은 재할당할 수 없지만, 내부의 속성이나 요소는 변경할 수 있음

  ```js
  const obj = { key: 'value' };
  obj.key = 'newValue'; // 가능
  console.log(obj.key); // 출력: newValue

  const arr = [1, 2, 3];
  arr.push(4); // 가능
  console.log(arr); // 출력: [1, 2, 3, 4]
  ```

<br>

## 정리

||스코프|재선언|재할당|호이스팅|
|---|---|---|---|---|
|**var**|함수 스코프|허용|가능|선언만 호이스팅 (초기화 X)|
|**let**|블록 스코프|불가|가능|호이스팅되나 TDZ 존재|
|**const**|블록 스코프|불가|불가능(단, 객체 내부 변경 가능)|호이스팅되나 TDZ 존재|