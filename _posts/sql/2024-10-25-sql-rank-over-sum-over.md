---
title:  "[SQL] 윈도우 함수 (RANK OVER, SUM OVER)"
excerpt: "SQL 윈도우 함수 (RANK OVER, SUM OVER)"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-25 18:27:30 +0900
last_modified_at: 2024-10-25 18:27:30 +0900
---

## RANK() OVER 함수

<br>

**```RANK()``` 함수는 데이터에 순위를 매기는 데 사용**  
**같은 값에는 동일 순위 부여**

```sql
RANK() OVER ( [PARTITION BY column] ORDER BY column [ASC|DESC] )
```

- ```ORDER BY```: 순위를 매길 기준 컬럼 지정하며, ```ASC```나 ```DESC```로 오름차순/내림차순을 설정 가능

- ```PARTITION BY```(옵션): 데이터를 그룹으로 나누어 각 그룹 내에서 별도로 순위를 매기고자 할 때 사용

<br>

### RANK() 예제

아래는 학생들의 성적에 따라 순위를 매기는 예제입니다.

**예제 테이블: students**

```
student_id  |    name           |   grade
------------------------------------------
1           |    John Doe       |   85
2           |    Jane Smith     |   92
3           |    Emily Davis    |   92
4           |    Michael Brown  |   78
5           |    Sarah Wilson   |   85
```

```RANK()```를 사용해 성적 순으로 순위 매기기

```sql
SELECT name, grade,
       RANK() OVER (ORDER BY grade DESC) AS ranking
FROM students;
```

**결과**

```
name          |  grade  |  ranking
-----------------------------------
Jane Smith    |  92     |  1
Emily Davis   |  92     |  1
John Doe      |  85     |  3
Sarah Wilson  |  85     |  3
Michael Brown |  78     |  5
```

위 결과에서 ```RANK()``` 함수는 동일한 성적(92, 85)을 가진 학생들에게 동일 순위를 부여하고, 건너 뛴 순위로 이어집니다.  
예를 들어, 성적이 92점인 두학생에게 1등을 부여하고, 85점인 학생에게 3등 부여.

<br>

<br>

## SUM() OVER 함수

<br>

**```SUM()``` 함수는 데이터의 합계를 계산.**  
**```OVER```와 함께 사용하면 행별 누적합을 계산합니다.**

```sql
SUM(column) OVER ( [PARTITION BY column] ORDER BY column [ROWS/RANGE BETWEEN])
```

- ```PARTITION BY```(옵션): 특정 그룹으로 데이터를 나누어 각 그룹의 합계를 계산합니다.

- ```ORDER BY```: 누적 계산의 순서를 지정합니다.

- ```ROWS BETWEEN``` 또는 ```RANGE BETWEEN```(옵션): 특정 범위 내 합계를 계산할 수 있습니다.

<br>

### SUM() OVER 예제

학생들의 성적에 따른 누적 합계 구하기

**예제 테이블: students**

```
student_id  |  name          | grade
--------------------------------------
1           |  John Doe      | 85
2           |  Jane Smith    | 92
3           |  Emily Davis   | 92
4           |  Michael Brown | 78
5           |  Sarah Wilson  | 85
```

```SUM() OVER```를 사용한 누적 합계

```sql
SELECT name, grade,
       SUM(grade) OVER (ORDER BY grade ASC) AS cumulative_grade
FROM students;
```

**결과**

```
name          |  grade |  cumulative_grade
-----------------------------------------
Michael Brown |  78    |  78
John Doe      |  85    |  163
Sarah Wilson  |  85    |  248
Jane Smith    |  92    |  340
Emily Davis   |  92    |  432
```

이 결과에서 ```SUM() OVER```는 ```grade```에 따라 오름차순으로 각 학생의 누적 성적을 계산합니다.

<br>

### SUM() OVER에 PARTITION BY를 사용한 예제

학과별로 성적의 누적 합계를 계산하는 예제입니다.

**예제 테이블: students (학과 추가)**

```
student_id  |  name          | grade  |  department
-----------------------------------------------------
1           |  John Doe      | 85     |  Computer Science
2           |  Jane Smith    | 92     |  Mathematics
3           |  Emily Davis   | 92     |  Mathematics
4           |  Michael Brown | 78     |  Computer Science
5           |  Sarah Wilson  | 85     |  Biology
```

```SUM() OVER()```에 ```PARTITION BY```를 사용해 학과별 누적 합계 구하기

```sql
SELECT name, department, grade,
       SUM(grade) OVER (PARTITION BY department ORDER BY grade ASC) AS cumulative_grade
FROM students;
```

**결과**

```
name           |  department        | grade  |  cumulative_grade
-----------------------------------------------------------------
Michael Brown  |  Computer Science  | 78     |  78
John Doe       |  Computer Science  | 85     |  163
Sarah Wilson   |  Biology           | 85     |  85
Jane Smith     |  Mathematics       | 92     |  92
Emily Davis    |  Mathematics       | 92     |  184
```
