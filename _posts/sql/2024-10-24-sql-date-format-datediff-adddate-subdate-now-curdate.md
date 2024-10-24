---
title:  "[SQL] 날짜 함수 (DATE, DATE_FORMAT, DATEDIFF, ADDDATE, SUBDATE, NOW, CURDATE)"
excerpt: "SQL 날짜 함수 (DATE, DATE_FORMAT, DATEDIFF, ADDDATE, SUBDATE, NOW, CURDATE) 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-24 23:46:30 +0900
last_modified_at: 2024-10-24 23:46:30 +0900
---

## DATE 함수

<br>

**```DATE``` 함수는 문자열 또는 다른 형식의 날짜 값을 표준 날짜 형식(```YYY-MM-DD```)으로 변환할 때 사용**

```sql
DATE(날짜 값 또는 문자열)
```

<br>

**예시**

```sql
SELECT DATE('2024-10-21 14:35:00') AS formatted_date;
```

![select-date](https://github.com/user-attachments/assets/b611793c-b8b7-4eaa-88b9-42c8862bb448)

위 쿼리는 시간 정보가 포함된 날짜 문자열에서 날짜 부분만 추출하여 표준 형식으로 변환  
**```DATE``` 함수는 시간 정보를 잘라내고 날짜를 반환**

<br>

```sql
SELECT name, DATE(enrollment_year)
FROM students;
```

이런식으로 날짜 부분만 추출할 때 이용할 수 있습니다.

<br>

<br>

## DATE_FORMAT 함수

<br>

**```DATE_FORMAT``` 함수는 날짜 형식을 사용자가 원하는 형식으로 변환할 수 있게 해주는 함수**

```sql
DATE_FORMAT(날짜 값, 형식)
```

```%Y```: 4자리 연도 (예: 2024)  
```%m```: 2자리 월 (예: 10)  
```%d```: 2자리 일 (예: 21)  
```%W```: 요일 (예: Monday)  
```%H```: 2자리 시간 (24시간 형식)  
```%i```: 2자리 분  
```%s```: 2자리 초

<br>

**예시**

```sql
SELECT DATE_FORMAT('2024-10-21', '%M %d, %Y') AS formatted_date;
```

![date-format](https://github.com/user-attachments/assets/b1b5fc62-9b43-4f81-bb2a-30b4ad9f2d0e)

위 쿼리는 ```DATE_FORMAT```을 사용해 날짜를 보기 좋게 변환합니다.  
```%M```은 월의 영어 이름, ```%d```는 2자리 일(day), ```%Y```는 4자리 연도를 표시합니다.

<br>

또 다른 예시로 학생 테이블의 등록 연도를 다른 형식으로 표시할 수 있습니다.

```sql
SELECT name, DATE_FORMAT(enrollment_year, '%Y-%m-%d') AS formatted_enrollment_year
FROM students;
```

**결과:**

```sql
name        formatted_enrollment_year
-------------------------------------
John Doe    2022-01-01
Jane Smith  2021-01-01
...
```

<br>

<br>

## DATEDIFF 함수

<br>

**```DATEDIFF``` 함수는 두 날짜간의 차이를 일(day) 단위로 계산합니다.```

```sql
DATEDIFF(날짜1, 날짜2)
```

<br>

**예시**

```sql
SELECT DATEDIFF('2024-10-21', '2024-10-01') AS date_difference;
```

![datediff](https://github.com/user-attachments/assets/d52ffb3a-099c-4911-836b-7d3492e5cd16)

```2024-10-21```와 ```2024-10-01```의 날짜 차이를 일 단위로 계산해 20일을 반환합니다.

<br>

학생 테이블에서 등록일과 현재 날짜 간의 차이를 계산할 때도 활용할 수 있습니다.

```sql
SELECT name, DATEDIFF(CURDATE(), enrollment_year) AS days_enrolled
FROM students;
```

**결과:**

```sql
name        days_enrolled
-------------------------
John Doe    660
Jane Smith  1025
...
```

이 쿼리는 ```CURDATE()```(현재날짜 반환) 함수로 현재 날짜에서 등록일 차이를 계산해 보여줍니다.

<br>

<br>

## ADDDATE 와 SUBDATE

<br>

- **ADDDATE: 특정 날짜에 일(day)을 더할 때 사용.**
- **SUBDATE: 특정 날짜에서 일(day)을 뺄 때 사용.**

```sql
ADDDATE(날짜, 일)
SUBDATE(날짜, 일)
```

<br>

**ADDDATE 예시**

```sql
SELECT ADDDATE('2024-10-21', 10) AS new_date;
```

**결과:**

```sql
new_date
----------
2024-10-31
```

<br>

**SUBDATE 예시**

```sql
SELECT SUBDATE('2024-10-21', 5) AS new_date;
```

**결과:**

```sql
new_date
----------
2024-10-16
```

<br>

<br>

## NOW와 CURDATE

<br>

- NOW(): 현재 날짜와 시간을 반환.
- CURDATE(): 현재 날짜만 반환.

<br>

**예시**

```sql
SELECT NOW() AS NOW_FUNC, CURDATE() AS CUR_FUND;
```

![now-curdate](https://github.com/user-attachments/assets/30be219c-a4ac-4db1-9831-e187086f9d82)

```NOW()``` 함수는 현재 날짜와 시간을, ```CURDATE()``` 함수는 날짜만 나타내는 것을 알 수 있습니다.
