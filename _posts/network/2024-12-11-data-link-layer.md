---
title:  "[Network] OSI 2계층 데이터링크 계층 (Data Link Layer)"
excerpt: "[Network] OSI 2계층 데이터링크 계층 (Data Link Layer)"

categories:
  - Network
tags:
  - [Network]

toc: true
toc_sticky: true
 
date: 2024-12-11 22:34:30 +0900
last_modified_at: 2024-12-11 22:35:30 +0900
---

## OSI 2계층: 데이터 링크 계층

<br>

네트워크 모델에서 데이터 링크 계층은 물리 계층과 상위 계층 사이에서 데이터를 효율적이고 안정적으로 전송하기 위한 핵심적인 역할을 수행합니다.

<br>

### 데이터 링크 계층의 역할

<br>

데이터 링크 계층은 네트워크에서 두 노드 간 신뢰할 수 있는 데이터 전송을 보장합니다.

이 계층은 프레임(Frame) 단위로 데이터를 처리하며, 물리 계층에서 발생할 수 있는 오류를 감지하고 수정합니다.

- 프레임화(Framing): 데이터 스트림을 일정한 크기의 프레임으로 나누어 전송합니다.

- 주소 지정(Addressing): 송신자와 수신자를 식별하기 위해 MAC 주소를 사용합니다.

- 오류 검출 및 수정(Error Detection and Correction): 전송 중 발생할 수 있는 데이터 손상을 검출하고 처리합니다.

- 흐름 제어(Flow Control): 데이터 송수신 속도를 조정하여 네트워크 혼잡을 방지합니다.

- 액세스 제어(Access Control): 여러 장치가 동일한 네트워크 매체를 사용할 때 충돌을 방지합니다.

<br>

### 데이터 링크 계층의 구성

<br>

데이터 링크 계층은 일반적으로 두 개의 하위 계층으로 나뉩니다.

#### MAC(Media Access Control) 하위 계층

MAC 하위 계층은 네트워크 매체에 대한 접근을 제어합니다.

MAC 주소: 네트워크 인터페이스에 고유하게 부여된 6바이트 주소로, 장치를 식별합니다.

CSMA/CD(Carrier Sense Multiple Access with Collision Detection): 충돌 방지를 위한 액세스 제어 메커니즘으로, 이더넷 환경에서 널리 사용됩니다.

프레임 전송 및 수신: 프레임을 매체에 전송하거나 수신하여 상위 계층으로 전달합니다.

#### LLC(Logical Link Control) 하위 계층

LLC 하위 계층은 데이터 링크 계층과 네트워크 계층 간 인터페이스를 제공합니다.

프로토콜 다중화: 여러 프로토콜 간 데이터를 구분합니다.

오류 검출: 데이터 손실 및 손상을 확인합니다.

<br>

### 이더넷 프레임의 구조

<br>


프리앰블(Preamble): 송수신 간 동기화를 위한 8바이트 크기의 정보입니다.

- 첫 7바이트: 10101010

- 마지막 바이트: 10101011

수신지 MAC 주소: 데이터를 받을 장치의 고유 MAC 주소(6바이트)입니다.

송신지 MAC 주소: 데이터를 보내는 장치의 고유 MAC 주소(6바이트)입니다.

타입/길이(Type/Length) 필드: 상위 계층 프로토콜 타입 또는 데이터 길이를 나타냅니다.

데이터: 상위 계층에서 전달받은 데이터이며, 최소 46바이트 이상이어야 합니다.  
부족할 경우 패딩으로 채웁니다.

FCS(Frame Check Sequence): CRC(Cyclic Redundancy Check) 값을 포함하며, 오류 검출을 위해 사용됩니다.

<br>

### 데이터 링크 계층에서의 오류 검출

<br>

CRC(Cyclic Redundancy Check): 프레임 끝에 추가되는 FCS 필드에 포함된 값으로, 데이터 무결성을 확인합니다.

ACK(응답 프레임): 수신 측에서 송신 측으로 데이터 수신 상태를 알리는 방식입니다.