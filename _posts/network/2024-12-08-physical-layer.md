---
title:  "[Network] OSI 1계층 물리 계층 (Physical Layer)"
excerpt: "[Network] OSI 1계층 물리 계층 (Physical Layer)"

categories:
  - Network
tags:
  - [Network]

toc: true
toc_sticky: true
 
date: 2024-12-08 22:14:30 +0900
last_modified_at: 2024-12-08 22:15:30 +0900
---

## OSI 7계층이란?

<br>

OSI(Open Systems Interconnection) 7계층 모델은 네트워크 통신을 표준화하기 위해 국제 표준화 기구(ISO)에서 제안한 모델입니다.

각 계층은 독립적으로 동작하며, 상위 계층은 하위 계층의 서비스를 이용하여 데이터를 전송합니다.

- **물리 계층 (Physical Layer)**: 전기적 신호와 물리적 매체를 다룸.

- **데이터링크 계층 (Data Link Layer)**: 오류 검출 및 수정, 프레임화 등을 담당.

- **네트워크 계층 (Network Layer)**: 패킷의 라우팅과 주소 지정.

- **전송 계층 (Transport Layer)**: 신뢰성 있는 데이터 전송 및 흐름 제어.

- **세션 계층 (Session Layer)**: 세션 유지 및 관리.

- **표현 계층 (Presentation Layer)**: 데이터 형식 변환과 암호화.

- **응용 계층 (Application Layer)**: 사용자와 직접 상호작용하는 애플리케이션.

<br>

<br>

## 물리 계층이란?

<br>

**물리 계층은 하드웨어적인 데이터 전송을 담당하는 계층입니다.**

**기본 정의**: 데이터를 0과 1로 이루어진 비트(bit) 형태로 변환하여 송신하거나 수신하는 역할을 합니다.

**주요 목적**: 데이터를 물리적 매체(케이블, 전파 등)를 통해 정확하게 전송하는 것.

<br>

### 물리 계층의 주요 기능

<br>

#### 데이터 전송

데이터를 아날로그 신호 또는 디지털 신호로 변환하여 전송합니다.  
아날로그 신호: 전파나 음성을 통해 데이터를 전송.  
디지털 신호: 전기 펄스(0과 1)로 데이터를 전송.  
예: 컴퓨터와 공유기 간의 데이터 교환.

<br>

#### 전송 매체 관리

데이터가 전달될 물리적 경로를 관리합니다.  
유선 매체: UTP 케이블, 광섬유.  
무선 매체: Wi-Fi, 블루투스.  

<br>

#### 신호 변환 및 복구

데이터를 송신할 때 전기 신호로 변환하고, 수신 시 원래 데이터로 복구합니다.  
왜 중요할까?  
네트워크 환경에 따라 신호가 약해질 수 있으므로 이를 복구하는 과정이 필요합니다.  

<br>

#### 전송 속도와 대역폭 관리

네트워크의 속도와 전송 용량을 설정합니다.  
예: Ethernet(이더넷)에서 10Mbps, 100Mbps, 1Gbps와 같은 속도 조정.  

<br>

### 물리 계층의 예시

<br>

#### 하드웨어 장치

허브(Hub): 네트워크에서 데이터를 단순히 전달하는 장치.  
리피터(Repeater): 약해진 신호를 증폭하여 전달.  
네트워크 케이블: 데이터를 물리적으로 전달.

<br>

#### 전송 매체

UTP 케이블: 흔히 사용하는 이더넷 케이블.  
광섬유 케이블: 빛을 이용해 데이터를 빠르게 전송.  
Wi-Fi 신호: 무선으로 데이터를 전송.

<br>

#### 통신 기술

Bluetooth: 짧은 거리에서 데이터 전송.  
5G: 고속 무선 데이터 전송 기술.