---
title:  "[SQL] 피벗 테이블"
excerpt: "SQL 피벗 테이블 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-25 21:40:30 +0900
last_modified_at: 2024-10-25 21:40:30 +0900
---

<br>

**SQL에서는 ```CASE WHEN```, ```IF```문과 집계 함수(```SUM```, ```MAX```, ```AVG```)를 사용해 피벗 테이블 구현합니다.**  
**피벗 테이블은 데이터를 집계하여 행과 열로 요약된 형태로 표현할 수 있게 해줍니다.**

<br>

**예시: 학생별 과목 성적을 피벗 테이블로 정리**

```sql
SELECT student_id,
       MAX(CASE WHEN subject = 'Math' THEN grade END) AS Math,
       MAX(CASE WHEN subject = 'Science' THEN grade END) AS Science,
       MAX(CASE WHEN subject = 'English' THEN grade END) AS English
FROM student_grades
GROUP BY student_id;
```

![pivot-max](https://github.com/user-attachments/assets/7a561b8a-c64f-410e-b13a-d6ddd73eeb80)

- ```CASE WHEN```을 사용해 과목별로 ```grade```값 추출

- ```MAX```함수는 동일한 ```student_id```를 가진 행을 하나로 합침

- ```GROUP BY student_id```를 통해 학생별로 데이터 집계
