---
title:  "[SQL] IF, CASE, NULL, COALESCE"
excerpt: "SQL IF, CASE, NULL, COALESCE 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-22 22:30:10 +0900
last_modified_at: 2024-10-22 22:30:10 +0900
---

## IF 함수

<br>

**```IF```함수는 조건식이 참일 때와 거짓일 때 다른 값을 반환**

```sql
IF(조건식, 참일 때 값, 거짓일 때 값)
```

<br>

**예시: 성적에 따라 합격 여부 표시하기**

```sql
SELECT name,
       grade,
       IF(grade >= 3.0, '합격', '불합격') AS result
FROM students;
```

![if-grade](https://github.com/user-attachments/assets/d8d5a5cf-c5e2-49ce-9793-a1ce6f6f9d79)

```IF```함수를 사용해 성적이 3.0이상인 경우엔 '합격', 아니면 '불합격'을 result에 출력하도록 작성

<br>

<br>

## CASE문

<br>

**```CASE```문은 SQL에서 더 복잡한 조건일 때 사용**

```sql
CASE
    WHEN 조건식1 THEN 반환값1
    WHEN 조건식2 THEN 반환값2
    ...
    ELSE 기본값
END
```

<br>

**예시: 성적에 따른 등급 표시**

```sql
SELECT name,
       grade,
       CASE
           WHEN grade >= 3.7 THEN 'A'
           WHEN grade >= 3.3 THEN 'B'
           WHEN grade >= 3.0 THEN 'C'
           ELSE 'D'
       END AS grade_level
FROM students;
```

![case-when-then-grade](https://github.com/user-attachments/assets/3626d5b1-6097-4bb3-be27-235d56d41bfe)

```CASE```문의 ```ELSE```로 모든 조건에 해당하지 않는 경우 반환할 값을 설정할 수 있다.

<br>

<br>

## NULL값 처리: ```NULL```과 ```COALESCE```

<br>

**데이터베이스의 ```NULL```은 값이 없음을 의미합니다.**

<br>

<br>

### NULL의 특성

<br>

```NULL```은 값이 존재하지 않음을 의미합니다.  
그래서 ```NULL```은 숫자나 문자열과 비교할 수 없습니다.

<br>

**잘못된 예**

```sql
SELECT *
FROM students
WHERE grade = NULL;
```

```NULL```은 어떤 값과도 같지 않기 때문에, 어떤 결과도 반환하지 않습니다.  
```NULL```값과 비교를 하려면 ```IS NULL``` 또는 ```IS NOT NULL```을 사용해야 합니다.

<br>

**예시: ```IS NULL```을 이용한 쿼리**

```sql
SELECT name
FROM students
WHERE grade IS NULL;
```

이 쿼리는 grade 값이 ```NULL```인 학생을 조회하는 방법

<br>

<br>

### COALESCE 함수

<br>

**```COALESCE``` 함수는 여러인자 중 ```NULL```이 아닌 첫 번째 값 반환**

```sql
COALESCE(값1, 값2, 값3, ...)
```

![coalesce-example](https://github.com/user-attachments/assets/20161e81-6d09-4c13-86e9-1302cee061b2)

<br>

**예시: ```NULL```인 성적을 0으로 대체**

```sql
SELECT name,
       COALESCE(grade, 0) AS grade
FROM students;
```

```grade```값이 ```NULL```인 경우 0을 반환하도록 작성.  
```COALESCE```는 여러 값 중 ```NULL```이 아닌 첫 번째 값을 반환하므로,  
여기서는 ```grade``` 값이 존재하면 ```grade```값 반환, 존재하지 않으면 0을 반환.
