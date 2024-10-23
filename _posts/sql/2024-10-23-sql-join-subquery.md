---
title:  "[SQL] INNER JOIN, LEFT JOIN, 서브쿼리(SUBQUERY)"
excerpt: "SQL INNER JOIN, LEFT JOIN, 서브쿼리(SUBQUERY) 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-23 23:09:10 +0900
last_modified_at: 2024-10-23 23:09:10 +0900
---

## JOIN

<br>

**JOIN은 여러 테이블의 데이터를 결합할 때 사용됩니다.**  
**JOIN은 ```INNER JOIN```과 ```LEFT JOIN```이 있습니다.**

<br>

### INNER JOIN


**```INNER JOIN```은 두 테이블 모두 조건에 맞는 데이터만 반환.**

<br>

**예시: 학생과 과목 테이블 결합**

```sql
SELECT students.name, courses.course_name
FROM students
INNER JOIN courses ON students.student_id = courses.student_id;
```

![inner-join](https://github.com/user-attachments/assets/f993373c-09aa-45f3-a350-34b8cc9d3f33)

이 쿼리는 ```students```테이블과 ```courses```테이블에서 학생 ID를 기준으로 매칭되는 학생의 이름과 과목 이름을 가져옵니다.

<br>

### LEFT JOIN


**```LEFT JOIN```은 왼쪽 테이블에 있는 모든 행을 반환하고, 오른쪽 테이블에서 일치하는 값이 있으면 함께 반환**  
**일치하는 값이 없을 경우 오른쪽 테이블의 값은 ```NULL```로 채워집니다.**

<br>

**예시: 과목 수강 내역이 없는 학생 포함**

```sql
SELECT students.name, courses.course_name
FROM students
LEFT JOIN courses ON students.student_id = courses.student_id;
```

이 쿼리는 모든 학생들을 조회하면서 과목 정보를 결합합니다.  
수강하지 않는 학생은 ```NULL```로 표시됩니다.

<br>

<br>

## 서브쿼리(SUBQUERY)

<br>

**서브쿼리는 쿼리 내에 포함된 또 다른 쿼리입니다.**  
**주로 복잡한 쿼리에서 중간 데이터를 처리하거나 특정 조건을 만족하는 데이터를 추출하기 위해 사용됩니다.**

<br>

**예시1: 각 학생이 수강한 과목 수 조회**

```sql
SELECT name,
       (SELECT COUNT(*)
        FROM courses
        WHERE courses.student_id = students.student_id) AS course_count
FROM students;
```

![select-subquery](https://github.com/user-attachments/assets/a77c9a4d-6f6d-4874-9d95-8a08a234fbda)

```students``` 테이블의 각 학생에 대해, 그 학생이  수강한 과목 수를 서브쿼리로 계산하여 ```course_count```라는 별칭으로 표시

<br>

**예시2: 평균 학점보다 높은 학생 조회**

```sql
SELECT name, grade
FROM students
WHERE grade> (
      SELECT AVG(grade)
      FROM students
);
```

![where-grade-subquery](https://github.com/user-attachments/assets/2c4c90b5-5fcb-412d-bcef-e5174ad1154a)

```students``` 테이블의 전체 학생 평균 학점을 계산한 후, 그보다 높은 학점을 가진 학생을 조회하는 방식

<br>

**예시3: 특정 과목을 수강한 학생 조회**

```sql
SELECT name
FROM students
WHERE student_id IN (
      SELECT student_id
      FROM courses
      WHERE course_name = 'Database Systems'
);
```

![where-student-id-in-subquery](https://github.com/user-attachments/assets/10a65292-acf7-4010-974d-afb289616d8c)

```course``` 테이블에서 'Database Systems' 과목을 수강한 학생의 ```student_id```를 가져온 뒤, 그 ID에 해당하는 학생의 이름을 ```student``` 테이블에서 조회하는 방식입니다.
