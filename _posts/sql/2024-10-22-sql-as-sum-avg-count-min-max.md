---
title:  "[SQL] AS, 숫자 연산(+,-,*,/), SUM, AVG, COUNT, MIN, MAX"
excerpt: "SQL AS, (+,-,*,/), SUM, AVG, COUNT, MIN, MAX에 대해 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-22 17:23:10 +0900
last_modified_at: 2024-10-22 17:23:10 +0900
---

## AS (컬럼 이름 변경)

<br>

**쿼리 결과에 나오는 컬럼 이름을 보기 쉽게 변경할 때 ```AS``` 사용**  
**결과에만 그렇게 나오는 것이며, 실제 데이터베이스 테이블의 컬럼 이름 바꾸는 것 아님**

```sql
SELECT 컬럼명 AS 새로운_이름
FROM 테이블명;
```

<br>

**예시**

학생을 조회할 때, name과 grade를 "이름"과 "성적"으로 표시하고 싶은 경우, ```AS```를 이용하면 됩니다.

```sql
SELECT name AS '이름',
       grade AS '성적'
FROM students;
```

![name-as-grade-as](https://github.com/user-attachments/assets/e1e41d8c-c444-4f8f-91d2-8142a8b5c6f1)

<br>

<br>

## 숫자 연산 (```+```, ```-```, ```*```, ```/```)

<br>

**데이터를 조회할 때 ```+```, ```-```, ```*```, ```/```으로 연산이 가능합니다.**

```sql
SELECT 컬럼1 연산자 컬럼2
FROM 테이블명;
```

<br>

**예시**

학생의 성적을 10% 올려서 보여주고 싶다면, ```*```를 이용할 수 있습니다.

```sql
SELECT name,
       grade * 1.1 AS '상승된 성적'
FROM students;
```

![grade-10](https://github.com/user-attachments/assets/e2bc5c76-7dc5-4bd9-b28a-118d25c524c3)

<br>

<br>

## 집계 함수 (```SUM```, ```AVG```, ```COUNT```, ```MIN```, ```MAX```)

<br>

**집계 함수는 데이터를 요약하고 분석할 때 유용**

- ```SUM()```: 값의 합계를 계산
- ```AVG()```: 값의 평균을 계산
- ```COUNT()```: 행의 개수를 계산
- ```MIN()```: 값 중 가장 작은 값 찾기
- ```MAX()```: 값 중 가장 큰 값 찾기

<br>

### ```SUM()```: 합계

학생들의 성적 총합을 ```SUM()```을 이용해서 알 수 있습니다.

```sql
SELECT SUM(grade) AS '성적 합계'
FROM students;
```

![sum-grade](https://github.com/user-attachments/assets/57afd032-bf7b-4369-969c-f2c0b91fa67e)

<br>

### ```AVG()```: 평균

학생들의 성적 평균을 구하려면 ```AVG()``` 함수를 사용할 수 있습니다.

```sql
SELECT AVG(grade) AS '평균 성적'
FROM students;
```

![avg-grade](https://github.com/user-attachments/assets/87c8d8d6-dead-4de4-ae7a-b2e5c4559688)

<br>

### ```COUNT()```: 개수

```COUNT()```는 데이터의 개수를 계산할 때 사용됩니다.  
예를 들어, 전체 학생 수를 알고 싶다면 아래와 같은 쿼리를 사용할 수 있습니다.

```sql
SELECT COUNT(*) AS '학생 수'
FROM students;
```

![count-students](https://github.com/user-attachments/assets/45929339-76b9-46a7-9169-2a2992e2b1e8)

<br>

특정 조건을 만족하는 학생 수를 계산할 수도 있습니다.  
예를 들어, 전공이 'Computer Science'인 학생수을 알고 싶다면, 아래와 같이 작성하면 됩니다.

```sql
SELECT COUNT(*) AS '컴퓨터과학 전공 학생 수'
FROM students
WHERE major = 'Computer Science';
```

![count-major-computer-science](https://github.com/user-attachments/assets/e9aa9614-37cf-42c6-b509-6c7550d532ff)

<br>

### ```MIN()```: 최소값

학생들 중 가장 낮은 성적을 구할 때, ```MIN()``` 함수를 사용할 수 있습니다.

```sql
SELECT MIN(grade) AS '최저 성적'
FROM students;
```

![min-grade](https://github.com/user-attachments/assets/e4977328-4f6b-46a2-a6c1-1ee5054b810f)

<br>

### ```MAX()```: 최대값

반대로 가장 높은 성적을 구한다면, ```MAX()``` 함수를 사용합니다.

```sql
SELECT MAX(grade) AS '최고 성적'
FROM students;
```

![max-grade](https://github.com/user-attachments/assets/21c37462-a51c-4f05-8bd3-85d2b38a009e)
