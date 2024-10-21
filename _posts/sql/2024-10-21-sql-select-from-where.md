---
title:  "[SQL] select, from, where"
excerpt: "select, from, where에 대해 알기 쉽게 작성"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-21 18:50:10 +0900
last_modified_at: 2024-10-21 18:50:10 +0900
---

## SELECT와 FROM

<br>

**```SELECT```는 컬럼을 지정하는 구문입니다.**
**그리고 ```FROM```은 데이터를 가져올 테이블을 지정하는 구문입니다.**

<br>

```sql
SELECT name, age
FROM students;
```

![select-name-age](https://github.com/user-attachments/assets/dc83bb02-87c7-47da-b0bd-47c5554ce1b9)

예시는 ```students``` 테이블에서 ```name```과 ```age``` 컬럼의 데이터를 선택하여 보여줍니다.
만약 students 테이블의 모든 데이터를 보려면 ```*```을 사용할 수 있습니다.

<br>

```sql
SELECT *
FROM students;
```

![select-from](https://github.com/user-attachments/assets/719e3355-6468-455b-be57-f2e9a6a8f197)

위 구문은 ```students``` 테이블의 모든 컬럼을 조회합니다.

<br>

```sql
SELECT name, age
FROM employees;
```

![select-name-age-employees](https://github.com/user-attachments/assets/fd4bda24-4fc5-475e-a75e-de7a9253f6b3)

위 구문은 ```employees```테이블의 ```name```과 ```age```컬럼의 데이터를 선택하여 보여줍니다.

<br>

<br>

## WHERE

<br>

**```WHERE```은 조건문을 이용해 특정 조건에 맞는 데이터만 조회할 때 사용합니다.**

<br>

예를 들어, 나이가 20살인 학생들만 보고 싶다면, 아래와 같이 ```WHERE``` 절을 사용합니다.

```sql
SELECT name, age
FROM students
WHERE age = 20;
```

![where-age-20](https://github.com/user-attachments/assets/f3b717ea-1cac-4822-974b-5f1f301fe8ae)

이 쿼리는 ```students``` 테이블에서 나이가 20인 학생들의 이름과 나이만 조회합니다.  
조건은 ```=``` 같다, ```<>``` 다르다, ```>``` 크다, ```<``` 작다 등의 연산자를 이용할 수 있습니다.

<br>

### 특정 값과 일치하는 데이터 조회

```sql
SELECT name
FROM employees
WHERE department = 'HR';
```

![where-department-hr](https://github.com/user-attachments/assets/cd9b031f-0154-49c5-bf7e-5ef58c1a452e)

```employees``` 테이블에서 부서가 'HR'인 직원들의 이름만 조회합니다.

<br>

### 범위 내의 데이터 조회

```sql
SELECT name, age
FROM students
WHERE age BETWEEN 18 AND 22;
```

![where-age-between](https://github.com/user-attachments/assets/a005591e-2489-4711-a604-f3a6d739af44)

```BETWEEN```을 이용해 특정 범위 내의 데이터를 조회할 수 있습니다.  
이 구문은 나이가 18세에서 22세 사이인 학생들을 조회합니다.

<br>

### 여러 조건으로 조회

```sql
SELECT name, age
FROM students
WHERE age >= 18 AND age <= 22;
```

![where-age-and-age](https://github.com/user-attachments/assets/00c21324-7990-439b-bef8-0ec333cb5f1f)

두가지 이상의 조건을 쓰려면 ```AND```와 ```OR```을 사용할 수 있습니다.
이 쿼리는 18세 이상 22세 이하인 학생들의 데이터를 AND를 이용해서 가져옵니다.

<br>

**\* 파이썬처럼 비교 연산자 ```18<=age<=22```로 작성하면 안됨!**

```sql
SELECT name, age
FROM students
WHERE 18<=age<=20;
```
이렇게 작성할 경우 오류 메시지가 뜨거나, 정확하지 않은 값이 나옴

<br>

### 종합 예시

```sql
SELECT *
FROM employees
WHERE age > 30 AND department = 'Sales';
```

![age-30-and-department-sales](https://github.com/user-attachments/assets/f3dd2e00-8b5d-4223-9945-e77861187fd5)

```employees``` 테이블에서 나이가 30세보다 많으며, 부서가 'Sales'인 직원들의 정보를 모두 조회합니다.
