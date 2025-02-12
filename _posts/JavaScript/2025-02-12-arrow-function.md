---
title: "[JS] 화살표 함수(Arrow Function)"
excerpt: "JavaScript의 화살표 함수(Arrow Function) 사용방법 알아보기"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true

date: 2025-02-12 20:27:00 +0900
last_modified_at: 2025-02-12 20:27:30 +0900
---

## Arrow Function(화살표 함수)란?

JavaScript에서 Arrow Function(화살표 함수)은 ES6(ECMAScript 2015)에서 도입된 새로운 함수 표현식  
기존의 함수 표현식과 비교하여 더 간결하고 가독성이 뛰어난 문법을 제공합니다  
특히, this 바인딩에 대한 특징이 있어, 객체 메서드나 콜백 함수에서 유용하게 사용

<br>

### 기본 문법

```js
const functionName = (parameters) => {
    // 함수 본문
};
```

<br>

#### 예시

**기본적인 화살표 함수**

```js
const add = (a, b) => {
    return a + b;
};

console.log(add(2, 3)); // 5
```

<br>

**단일 표현식: 본문이 단일 표현식일 경우 중괄호와 return 키워드를 생략가능**

```js
const multiply = (a, b) => a * b;

console.log(multiply(2, 3)); // 6
```

<br>

**매개변수가 하나인 경우: 매개변수가 하나일 경우 괄호를 생략가능**

```js
const square = x => x * x;

console.log(square(4)); // 16
```

<br>

**매개변수가 없는 경우: 이 경우 빈 괄호를 사용**

```js
const greet = () => "Hello, World!";

console.log(greet()); // "Hello, World!"
```

<br>

<br>

### this 바인딩

화살표 함수의 가장 큰 특징 중 하나는 this 바인딩  
일반 함수는 호출되는 방식에 따라 this가 동적으로 결정되지만, 화살표 함수는 정의된 위치에서의 this 값을 lexically(정적으로) 캡처  
즉, 화살표 함수 내의 this는 외부 컨텍스트의 this를 그대로 사용합니다.

<br>

#### 예시

```js
function Person() {
    this.age = 0;

    setInterval(() => {
        this.age++; // 화살표 함수에서의 this는 Person 객체
        console.log(this.age);
    }, 1000);
}

const person = new Person(); // 1, 2, 3, ...
```

위 코드에서 setInterval의 콜백 함수가 화살표 함수로 정의되었기 때문에, this는 Person 객체를 가리킴  
반면 일반 함수를 사용했다면 this가 전역 객체를 가리키게 되어, 의도한 대로 동작하지 않았을 것

```js
// 일반 함수 예시
function Person() {
    this.age = 0;

    setInterval(function() {
        this.age++; // `this`는 전역 객체를 가리킴
        console.log(this.age);
    }, 1000);
}

const person = new Person(); // NaN (undefined + 1)
```

<br>

#### 사용 시 주의사항

**생성자 함수로 사용 불가**: 화살표 함수는 생성자 함수로 사용할 수 없음  
new 키워드와 함께 사용할 수 없으며, this를 캡처하기 때문에 인스턴스를 생성할 수 없음

```js
const Foo = () => {};
const foo = new Foo(); // TypeError: Foo is not a constructor
```

<br>

**arguments 객체 없음**: 화살표 함수 내에서는 arguments 객체가 존재하지 않기 때문에, 필요할 경우 Rest 매개변수(...args)를 사용해야 함

```js
const myFunc = (...args) => {
    console.log(args); // 모든 인수를 배열로 받음
};
myFunc(1, 2, 3); // [1, 2, 3]
```

일반 함수에서는 아래와 같이 함수에 전달된 모든 인수를 배열처럼 접근 가능

```js
function myFunction() {
    console.log(arguments); // 모든 인수를 포함한 객체
    console.log(arguments[0]); // 첫 번째 인수
}

myFunction(1, 2, 3); // 출력: [1, 2, 3]
                     //       1
```

하지만 화살표 함수는 아래와 같이 오류 발생

```js
const myArrowFunction = () => {
    console.log(arguments); // ReferenceError: arguments is not defined
};

myArrowFunction(1, 2, 3);
```