---
title: "다중 로봇 협력형 구호 로봇 시스템"
excerpt: "VicPinky 모선이 다수의 Turtlebot3를 운반하고, 협소 공간에 투입된 로봇이 자율 탐사로 요구조자를 식별해 구호품을 전달하는 통합 시스템."
date: 2026-07-09
domain: "Robotics"
accent: "#0d4fbd"
period: "2026.06.01 – 2026.07.09"
kind: "팀 프로젝트"
role: "Turtlebot3 개조 및 하드웨어 제어 패키지 개발"
repo: "https://github.com/ManticoreXL/vicpinky_carrier"
stack:
  - ROS2 Jazzy
  - C++
  - Python
  - Nav2
  - SLAM Toolbox
  - YOLO
  - OpenCV
  - TypeScript / React
header:
  overlay_color: "#0c2545"
  overlay_filter: "0.15"
tags:
  - ROS2
  - Robotics
  - SLAM
  - Computer Vision
---

{% include proj-meta.html %}

## 프로젝트 개요

재난 환경처럼 인력 투입이 어려운 협소 공간에 소형 탐사 로봇을 다수 전개하는 **구호 로봇 시스템**입니다.
모선 역할의 **VicPinky**가 여러 대의 **Turtlebot3**를 탑재·운반하고, 투입된 Turtlebot이 협소 공간에 진입해
요구조자를 탐색합니다. 요구조자를 식별한 뒤 구호품 전달까지 이어지는 전체 시퀀스를 자율적으로 수행하도록
하드웨어 개조부터 자율탐사, 관제 시스템까지 통합했습니다.

## 시스템 구성 (하드웨어)

- **PinkLAB VicPinky** — 모선. 다수의 탐사 로봇을 탑재·운반하고 경사로로 상하차를 수행
- **ROBOTIS Turtlebot3 Burger** — 협소 공간 진입용 탐사 로봇
- **ROBOTIS OMX Manipulator** — 구호품 적재용 매니퓰레이터

개발 환경은 **Ubuntu 24.04 LTS + ROS2 Jazzy Jalisco** 기반이며, 로봇 제어는 C/C++ · Python 패키지로,
관제용 대시보드는 TypeScript / React로 구현했습니다.

## 핵심 구현

### Turtlebot3 하드웨어 제어

탐사 환경에 대응할 수 있도록 Turtlebot에 **전조등 · 카메라 · 마이크 · 스피커**를 장착해 개조했습니다.

- `headlight_node` — 조명 제어 토픽을 구독하여 LED를 조작하고, 파라미터를 통해 설정값을 제어
- `voice_node` — 발화 토픽을 수신해 스피커로 **TTS**를 출력하고, 마이크로 음성을 감지하면 **STT**를 수행

### VicPinky 하드웨어 제어

- **경사로 제어 액션 서버** — 개방/폐쇄 목표를 수신하면 모터로 경사로를 자동으로 개폐
- **OMX Manipulator 모방학습** — 요구조자가 필요로 하는 구호품을 Turtlebot에 적재하도록 모방학습 적용

### 상하차 및 주차 메커니즘

- Turtlebot이 VicPinky 경사로 바닥의 선을 따라 **라인트레이싱**으로 안정적으로 상차
- 내부 카메라로 바닥의 마커와 Turtlebot의 마커를 인식해 **주차 위치를 보정**

### 자율탐사 및 요구조자 식별

- **SLAM Toolbox**로 협소 공간의 지도를 실시간 생성하고, **Nav2**로 자율 탐사 경로를 계획
- `mission_coordinator` 노드가 한정된 공간 내에서 **프론티어가 가장 많은 방향**으로 탐색을 지시
- **YOLO** 모델로 카메라 영상에서 요구조자를 실시간 탐지하고, 위치를 관제 시스템에 전달
