---
title:  "[SQL] GROUP BY, ORDER BY"
excerpt: "SQL GROUP BY, ORDER BY에 대해 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-22 18:08:10 +0900
last_modified_at: 2024-10-22 18:08:10 +0900
---

## GROUP BY

<br>

**```GROUP BY```는 데이터를 특정 기준으로 묶어, 각 그룹별로 집계할 수 있도록 해줍니다.**  
예를 들어, 전공별로 학생들의 성적을 집계하거나, 연도별로 등록한 학생 수를 계산할 때 사용할 수 있습니다.

<br>

**예시1: 전공별로 평균 성적 구하기**

```sql
SELECT major,
       AVG(grade) AS avg_grade
FROM students
GROUP BY major;
```

![group-by-major](https://github.com/user-attachments/assets/b746566c-3b47-4bd2-885f-30c28aca5756)

이 쿼리는 major(전공)별로 데이터를 묶고, 각 전공에 속한 학생들의 성적 평균을 계산합니다.

<br>

**예시2: 등록 연도별 학생 수 구하기**

```sql
SELECT enrollment_year,
       COUNT(*) AS student_count
FROM students
GROUP BY enrollment_year;
```

![group-by-enrollment-year](https://github.com/user-attachments/assets/a6e6559c-0d7f-4cad-8f44-d180c097456e)

<br>

<br>

## ORDER BY

<br>

**```ORDER BY```는 쿼리의 결과를 특정 컬럼을 기준으로 오름차순(```ASC```) 또는 내림차순(```DESC```)으로 정렬하는 기능입니다.**  
**기본은 오름차순으로, 명시하지 않을 경우 오름차순이 됩니다.**

<br>

**예시1: 성적이 높은 순서대로 학생 조회**

```sql
SELECT name, grade
FROM students
ORDER BY grade DESC;
```

![order-by-grade-desc](https://github.com/user-attachments/assets/edb7a049-13d9-4fbf-b814-8460908254e8)

```DESC```를 이용해 성적이 높은 순서대로 내림차순 정렬을 했습니다.

<br>

**예시2: 성적이 낮은 순서대로 학생 조회**

```sql
SELECT name, grade
FROM students
ORDER BY grade;
```

![order-by-grade](https://github.com/user-attachments/assets/ec524bf2-b13f-40fa-b217-4c4e295e354b)

성적이 낮은 순서부터 정렬이 되었습니다.  
여기서 알 수 있듯 ```ASC```를 쓰지 않아도 기본값이 오름차순이기 때문에, 오름차순으로 정렬되었습니다.

<br>

<br>

## ```GROUP BY```와 ```ORDER BY``` 함께 사용하기

<br>

**예시: 전공별 평균 성적을 내림차순으로 정렬**

```sql
SELECT major,
       AVG(grade) AS avg_grade
FROM students
GROUP BY major
ORDER BY avg_grade DESC;
```

![group-by-order-by](https://github.com/user-attachments/assets/3c4b105f-d7b5-468d-8096-6d7e70987707)

```GROUP BY```를 이용해 전공별로 성적 평균을 낸 뒤, ```ORDER BY```를 이용해 성적을 내림차순 정렬
