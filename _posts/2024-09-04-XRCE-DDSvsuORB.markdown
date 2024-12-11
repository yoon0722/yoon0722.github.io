---
layout: post
title:  "XRCE-DDS vs uORB"
date:   "2024-09-04 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["[Project] Drone"]
tags: ["XRCE-DDS", "uORB", "ROS2", "PX4"]

#classes: wide
#toc: true
#toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "XRCE-DDS vs uORB"
date: "2024-09-04 00:00:00 +0900"
last_modified_at: "2024-09-04 00:00:00 +0900"
categories:
  - Project
tags:
  - XRCE-DDS
  - uORB
  - drone
  - ROS2
  - PX4
author_profile: true
sidebar:
    nav: docs
---

### XRCE-DDS
- **"eXtremely Resource-Constrained Environments Data Distribution Service"**의 약자
- ROS2와 PX4 또는 다른 시스템간의 **외부 통신**을 위한 미들웨어
- 주로 리소스가 제한된 임베디드 시스템에서 DDS(Data Distribution Service) 프로토콜을 사용하여 데이터를 주고받기 위해 사용된다.

#### [특징]
- PX4와 외부시스템(ex.ROS2)간의 통신을 중계하는 미들웨어
- XRCE-DDS는 PX4 내부의 uORB 메시지를 변환해 ROS2 메시지로 송수신할 수 있다.
즉, PX4와 ROS2간의 데이터 흐름을 관리하는 역할을 한다.
- uORB에서 발행된 메시지를 외부로 전달하거나 외부 명령을 PX4로 전달할 때 사용된다.
- DDS는 분산 시스템간의 데이터 공유를 표준화한 프로토콜이다. 
XRCE-DDS는 이 DDS를 임베디드 시스템에서 사용할 수 있도록 경량화한 버전
- PX4에서 XRCE-DDS는 클라이언트로서 작동하고 ROS2나 다른 DDS 네트워크에 연결된 컴퓨터(Companion Computer)는 에이전트로 작동하여 데이터 통신을 중계한다.

---

### uORB
- **"Micro Object Request Broker"**의 약자
- PX4 **내부**에서 사용되는 프로세스 간 통신(IPC:Inter-Process Communication)을 위한 시스템이다.
- PX4의 여러 모듈(비행제어, 네비게이션 등)간에 데이터를 교환하기 위해 사용된다.

#### [특징]
- uORB는 PX4의 내부 모듈 간 실시간 통신을 담당하는 경량화된 메시징 시스템
- 리소스가 제한된 시스템에서 저지연 메시지 전달을 보장하도록 설계되었다.
실시간 비행 제어 시스템에서는 빠르고 효율적인 통신이 중요
- 메시지의 발행(Publish)과 구독(Subscribe) 메커니즘을 사용해 모듈들이 데이터를 주고받는다.
예시로 센서 모듈이 데이터를 발행하고, 비행 제어 모듈이 그 데이터를 구독하여 제어에 사용

<br/>

|특징|XRCE-DDS|uORB|
|:---|:---|:---|
|**주요 목적**|PX4와 **외부** 시스템(ROS 2 등) 간의 통신|PX4 **내부** 모듈 간의 통신|
|**통신 범위**|PX4와 **외부** 시스템(예: ROS 2) 간의 데이터 전송|PX4 **내부**에서 모듈 간의 데이터 전송|
|**기술 기반**|**DDS (Data Distribution Service)** 프로토콜 기반|**IPC (Inter-Process Communication)** 시스템|
|**사용 환경**|리소스 제한적인 환경에서의 분산 시스템 간 데이터 공유|실시간 임베디드 시스템(PX4) 내부의 데이터 공유|
|**데이터 흐름**|PX4 내부 -> XRCE-DDS -> 외부 시스템|PX4 모듈 간(센서 모듈 -> 제어 모듈)|
|**주요 활동**|ROS 2와 PX4 간의 메시지 교환 및 외부 제어 시스템 통합|PX4 내부에서 센서 데이터와 제어 명령을 교환|