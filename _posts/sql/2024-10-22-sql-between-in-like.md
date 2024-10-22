---
title:  "[SQL] BETWEEN, IN, LIKE"
excerpt: "SQL BETWEEN, IN, LIKE 구문에 대해 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-22 15:01:10 +0900
last_modified_at: 2024-10-22 15:01:10 +0900
---

## BETWEEN

<br>

**```BETWEEN```은 값이 특정 범위 내에 있는지 확인할 때 사용**

```sql
SELECT 컬럼1, 컬럼2
FROM 테이블명
WHERE 컬럼 BETWEEN 시작값 AND 끝값;
```

<br>

**예시**

학생의 나이가 20세 이상 22세 이하인 데이터 조회하기

```sql
SELECT name, age
FROM students
WHERE age BETWEEN 20 AND 22;
```

![age-between-20-and-22](https://github.com/user-attachments/assets/c963071b-20d3-4763-a6e4-f0d24b949856)

**```BETWEEN```은 범위의 시작 값과 끝 값도 포함**  
위 예시의 경우 20, 21, 22의 값을 조회합니다.

<br>

<br>

## IN

<br>

**```IN```은 지정된 값 목록 중 하나와 일치하는 데이터를 찾을 때 사용**  
**```OR``` 대신 ```IN```을 사용하면 간결하게 표연할 수 있습니다.**

```sql
SELECT 컬럼1, 컬럼2
FROM 테이블명
WHERE 컬럼 IN (값1, 값2, 값3, ...);
```

<br>

**예시**

전공이 'Computer Science', 'Physics', 'Mathematics' 중 하나인 학생들의 데이터를 조회

```sql
SELECT name, major
FROM students
WHERE major IN ('Computer Science', 'Physics', 'Mathematics');
```

![major-in](https://github.com/user-attachments/assets/009bc1e5-9619-40f0-8214-16ec232f01ad)

<br>

<br>

## LIKE

<br>

**```LIKE```는 문자열 데이터를 검색할 때 사용**  
**주로 와일드카드(```%```, ```_```)와 함께 사용**

- ```%```는 0개 이상의 문자를 의미
- ```_```는 정확히 하나의 문자를 의미

<br>

```sql
SELECT 컬럼1, 컬럼2
FROM 테이블명
WHERE 컬럼 LIKE '패턴';
```

<br>

**예시1**

이름이 'J'로 시작하는 학생 찾기

```sql
SELECT name
FROM students
WHERE name LIKE 'J%';
```

![like-j](https://github.com/user-attachments/assets/7038d6c2-750b-4536-93c2-e795bfec7d2b)

<br>

**예시2**

이름이 'a'로 끝나는 학생 찾기

```sql
SELECT name
FROM students
WHERE name LIKE '%a';
```

![like-a](https://github.com/user-attachments/assets/d060e61d-b8bf-4148-acd0-903274267977)

<br>

**예시3**

이름의 두번째 문자가 'a'인 학생 찾기

```sql
SELECT name
FROM students
WHERE name LIKE '_a%';
```

![like-2-a](https://github.com/user-attachments/assets/1a8ac45e-3284-44a9-92c6-fb1ac2304746)

<br>

**\* ```LIKE```는 대소문자를 구분하지 않음**

- ```Like 'J%"```는 'j'로 시작하는 데이터도 반환
