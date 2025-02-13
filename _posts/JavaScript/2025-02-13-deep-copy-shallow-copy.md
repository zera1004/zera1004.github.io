---
title: "[JS] 깊은 복사와 얕은 복사"
excerpt: "JavaScript의 깊은 복사와 얕은 복사란? 그리고 사용방법 알아보기"

categories:
  - JavaScript
tags:
  - [JavaScript]

toc: true
toc_sticky: true

date: 2025-02-13 20:15:00 +0900
last_modified_at: 2025-02-13 20:15:30 +0900
---

## 깊은 복사(Deep Copy)와 얕은 복사(Shallow Copy)

**얕은 복사(Shallow Copy)** 는 객체의 1차원 속성만 복사하는 방식.  
즉, 객체의 속성 중 기본 데이터 타입(숫자, 문자열, 불리언 등)은 값으로 복사되지만, 객체나 배열과 같은 참조 타입의 속성은 참조만 복사됨.  
따라서 원본 객체의 참조 타입 속성을 수정하면, 얕은 복사를 통해 생성된 객체에도 영향을 미침.

**깊은 복사(Deep Copy)** 는 객체의 모든 속성을 재귀적으로 복사하는 방식.  
이 방법은 원본 객체의 모든 속성과 하위 객체를 새로운 메모리 공간에 복사하므로, 원본 객체를 수정하더라도 깊은 복사된 객체에는 영향을 미치지 않음.

**즉, 배열과 객체의 경우 얕은 복사는 원본의 주소 값을 가져오는 것, 깊은 복사는 원본의 모든 속성과 값을 가져오는 것.**

<br>

### 얕은 복사 구현 방법

1. **Object.assign()**

```js
const original = { a: 1, b: { c: 2 } };
const shallowCopy = Object.assign({}, original);

shallowCopy.b.c = 3; // 원본 객체에도 영향을 미침
console.log(original.b.c); // 3
```

2. **전개 연산자(Spread Operator)**

```js
const original = { a: 1, b: { c: 2 } };
const shallowCopy = { ...original };

shallowCopy.b.c = 3; // 원본 객체에도 영향을 미침
console.log(original.b.c); // 3
```

3. **slice()**

```js
const originalArray = [{ a: 1 }, { b: 2 }];
const shallowCopy = originalArray.slice();

shallowCopy[0].a = 3; // 원본 배열에도 영향을 미침
console.log(originalArray[0].a); // 3
```

<br>

### 깊은 복사 구현 방법

1. **JSON.parse()와 JSON.stringify()**

```js
const original = { a: 1, b: { c: 2 } };
const deepCopy = JSON.parse(JSON.stringify(original));

deepCopy.b.c = 3; // 원본 객체에는 영향 없음
console.log(original.b.c); // 2
```

이 방법은 단순한 객체에 대해서는 잘 작동하지만, 함수, undefined, Date, Map, Set 등과 같은 특정 데이터 타입은 제대로 복사되지 않음.

2. **재귀 함수 사용**

```js
function deepClone(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj; // 기본 데이터 타입은 그대로 반환
    }

    const copy = Array.isArray(obj) ? [] : {}; // 배열인지 확인

    for (const key in obj) {
        copy[key] = deepClone(obj[key]); // 재귀 호출
    }

    return copy;
}

const original = { a: 1, b: { c: 2 } };
const deepCopy = deepClone(original);

deepCopy.b.c = 3; // 원본 객체에는 영향 없음
console.log(original.b.c); // 2
```

## 요약

- **얕은 복사**: 객체의 1차원 속성만 복사하며, 참조 타입 속성은 원본 객체와 동일한 메모리 주소를 참조.  
Object.assign()이나 전개 연산자, slice()를 통해 구현할 수 있음.

- **깊은 복사**: 객체의 모든 속성을 재귀적으로 복사하며, 원본 객체와 독립적인 새로운 객체를 생성.  
JSON.parse()와 JSON.stringify()를 사용하거나, 재귀 함수를 통해 구현할 수 있음.