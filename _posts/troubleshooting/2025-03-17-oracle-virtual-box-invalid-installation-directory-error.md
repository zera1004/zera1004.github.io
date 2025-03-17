---
title: "[Troubleshooting] 오라클 버츄얼 박스 invalid installation directory 에러"
excerpt: "[Troubleshooting] 오라클 버츄얼 박스 invalid installation directory 에러 생겼을 때 해결 방법"

categories:
  - Troubleshooting
tags:
  - [Troubleshooting]

toc: true
toc_sticky: true

date: 2025-03-17 16:15:10 +0900
last_modified_at: 2025-03-17 16:16:10 +0900
---

## Oracle VirtualBox 에러 발생

C드라이브 용량이 많이 남지 않아 D드라이브에 VirtualBox를 설치 하려는데

![Invalid installation directory 에러](https://github.com/user-attachments/assets/95109ca6-d3eb-48c5-a07b-04cd86d9fcb1)

Invalid installation directory
The chosen installation directory is invalid, as it does not meet the security requirements. Refer to the Oracle VirtualBox 7.1.6 manual for more information. Please choose another directory for installing' Oracle VirtualBox 7.1.6.

이런 에러가 떴다.  
찾아보니 보안상의 이유로 사용자의 수정, 쓰기 권한이 있는 폴더에 설치를 할 수 없는 것이었다.

<br>

## 해결 방법

![보안](https://github.com/user-attachments/assets/50a10199-ac74-42c4-8e55-98d8c52e63a3)

현재는 수정, 쓰기 권한 설정을 할 수가 없다.  
고급 버튼 클릭

![상속 사용 안함](https://github.com/user-attachments/assets/f3547be2-d610-46a5-9542-63f6fb2380fe)

상속 사용 안 함(L) 클릭

![권한 변환](https://github.com/user-attachments/assets/24d6070d-c88f-44b4-aaa1-8deebe02ff00)

상속된 사용 권한을 이 개체에 대한 명시적 사용 권환으로 변환합니다. 클릭  
그리고 확인 버튼을 눌려줍니다.

![설정 보안](https://github.com/user-attachments/assets/4d6a9bbb-b5e2-4662-aa0e-a09cee9c68d8)

이제 다시 돌아오면 권한 설정이 가능함으로 Authenticated Users 사용 권한을 변경하기 위해 편집 클릭

![권한 해제](https://github.com/user-attachments/assets/6d66096a-dc4b-4908-98c7-baca8edfeff0)

이제 수정과 쓰기 권한을 해제하고 다시 확인을 눌러주면 됩니다.

이제 설치가 가능해집니다.

설치를 하고 난 후에는 다시 수정과 쓰기 권한을 줘도 상관없는 것으로 확인했습니다.
