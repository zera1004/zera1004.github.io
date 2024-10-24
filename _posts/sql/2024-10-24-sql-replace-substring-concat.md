---
title:  "[SQL] REPLACE, SUBSTRING, CONCAT"
excerpt: "SQL REPLACE, SUBSTRING, CONCAT 알아보기"

categories:
  - SQL
tags:
  - [SQL]

toc: true
toc_sticky: true
 
date: 2024-10-24 18:06:30 +0900
last_modified_at: 2024-10-24 18:06:30 +0900
---

## REPLACE

<br>

**```REPLACE``` 함수는 문자열에서 특정 문자열을 다른 문자열로 치환할 때 사용**

```sql
REPLACE(원본 문자열, 찾을 문자열, 대체할 문자열)
```

<br>

**예시1**

```sql
SELECT REPLACE('Hello World', 'World', 'SQL') AS replace_text;
```

**결과:**

```sql
replaced_text
--------------
Hello SQL
```

위 커리는 'Hello World'라는 문자열에서 'World'라는 부분을 'SQL'로 바꾸어 'Hello SQL'이라는 결과를 반환합니다.

<br>

**예시2**

```sql
SELECT name,
       REPLACE(major, 'Science', 'Engineering') AS updated_major
FROM students;
```

![replace-major](https://github.com/user-attachments/assets/ec25e7fb-51a5-4fae-b826-2fd0ec790add)

위 커리는 전공(major) 이름 중 'Science'가 들어간 부분을 'Engineering'으로 바꿉니다.

<br>

<br>

## SUBSTRING 함수

<br>

**```SUBSTRING``` 함수는 문자열의 일부를 추출할 때 사용.**  
**시작 위치와 길이를 지정하여 원하는 부분만 선택할 수 있습니다.**

```sql
SUBSTRING(원본 문자열, 시작 위치, 추출할 길이)
```

**```SUBSTRING``` 대신에 ```SUBSTR```을 써도 됨**

<br>

**예시1**

```sql
SELECT SUBSTRING('Hello SQL World', 7, 3) AS substring_text;
```

**결과:**

```sql
substring_text
---------------
SQL
```

위 커리는 'Hello SQL World'라는 문자열에서 7번째 문자부터 시작해 3글자를 추출해 'SQL'을 반환합니다.

<br>

**예시2: 학생 이름에서 성만 추출**

```sql
SELECT name,
       SUBSTRING(name, 1, LOCATE(' ', name) -1) AS last_name
FROM students;
```

![substring-name](https://github.com/user-attachments/assets/f993e067-ea84-4801-bbc8-13542bbb0aff)

```SUBSTRING```과 ```LOCATE```함수를 조합해 이름에서 첫번째 공백이 나오기 전까지의 문자를 추출해 성을 가져옵니다.  
```LOCATE(찾을 문자, 원본 문자열)```방식으로, 찾을 문자의 위치를 반환합니다.

<br>

<br>

## CONCAT 함수

<br>

**```CONCAT```함수는 여러개의 문자열을 하나로 연결할 때 사용됩니다.**

```sql
CONCAT(문자열1, 문자열2, ..., 문자열N)
```

<br>

**예시1**

```sql
SELECT CONCAT('Hello, ', 'SQL World!') AS concat_text;
```

**결과:**

```sql
concat_text
------------
Hello, SQL World!
```

'Hello, '와 'SQL World!'라는 두 문자열을 결합해 하나의 문장으로 만듭니다.

<br>

**예시2**

```sql
SELECT CONCAT(name, ' is majoring in ', major) AS student_info
FROM students;
```

![concat-name-major](https://github.com/user-attachments/assets/316c20ed-d49d-4122-b8e2-1af39a27dea2)

```CONCAT```을 사용하여 학생 이름과 전공을 하나의 문장으로 결합한 결과를 출력합니다.
