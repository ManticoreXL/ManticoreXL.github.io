---
title: "투구 및 타격 자세 분석 시스템"
excerpt: "YOLOv8 Pose로 신체 랜드마크를 추출하고, 프로 선수 자세를 학습한 딥러닝 모델로 사용자 자세를 비교·분석하는 컴퓨터비전 웹 서비스."
date: 2026-03-19
domain: "AI · Vision"
accent: "#6a4bbd"
period: "2026.03.06 – 2026.03.19"
kind: "팀 프로젝트"
role: "데이터 전처리·학습, 웹 백엔드, 라우터, 모델 API 개발"
repo: "https://github.com/ManticoreXL/AI_Pitching_analysis_system"
stack:
  - Python
  - Flask
  - YOLOv8 Pose
  - TensorFlow / Keras
  - MediaPipe
  - SQLite3
  - Raspberry Pi 5
header:
  overlay_color: "#0c2545"
  overlay_filter: "0.15"
tags:
  - AI
  - Computer Vision
  - Backend
  - Deep Learning
---

{% include proj-meta.html %}

## 프로젝트 개요

투구나 타격처럼 **역동적인 자세**를 정량적으로 분석할 수 있는 시스템의 필요성에서 출발했습니다.
컴퓨터비전과 인공지능 모델을 통해 자세를 데이터로 분석·평가하고, 그 결과를 사용자에게 직관적으로
제공하는 **웹 기반 서비스**를 목표로 했습니다.

> 사용 기술: Python · Flask · SQLite3 · Ultralytics YOLOv8 Pose · MediaPipe · TensorFlow Keras · Raspberry Pi 5

## 핵심 구현

### 데이터 수집 및 모델 학습

- 프로 선수들의 투구·타격 영상을 수집해 **YOLO Pose**로 신체 랜드마크 식별
- 딥러닝 모델이 학습할 수 있도록 **스켈레톤 데이터**로 추출하여 수집
- 일관성 있는 학습을 위해 데이터 **규격화 및 전처리 알고리즘** 적용
- 프로 선수 자세를 학습한 **Keras 기반 모델**로 사용자 자세에서 특징을 추출·비교

### 백엔드 및 API

- **Python Flask** 프레임워크 기반으로 웹 서버 라우터와 백엔드 API 설계
- 영상 분석 결과 및 프로 선수 정보를 관리하기 위해 **데이터베이스 연동**
- 모델 추론의 동시성을 보장하기 위해, 요청 후 추론을 **백그라운드 비동기**로 처리

### 시스템 통합 및 배포

- 사용자 영상을 분석해 **어떤 선수와 가장 유사한지** 출력
- 반응형 웹 구조로 설계해 PC와 모바일 모두에서 유연하게 사용 가능
- **Cloudflare** 스마트 라우팅으로 서버 구동 후 외부 배포

## 트러블슈팅

<div class="ts" markdown="1">
<div class="ts__head"><span class="ts__tag">Trouble</span>랜드마크 추출 모델 교체 — MediaPipe → YOLOv8 Pose</div>
<dl>
<dt>문제</dt>
<dd>초기 파이프라인은 MediaPipe로 신체 랜드마크를 추출했으나, 타격 자세 분석을 추가하는 과정에서 관절 추적이 불안정함을 인지. 신체 부위가 서로 겹쳐 가려지는 상황에서 추적이 끊기고 CSV 데이터에 값이 누락됨.</dd>
<dt>원인</dt>
<dd>MediaPipe는 신체 부위가 가려지는 상황에 취약해 관절 추적이 끊기고 좌표값을 놓치는 한계가 있었음. 이로 인해 수집 데이터 품질이 저하되고 모델 학습에도 부정적 영향을 줌.</dd>
<dt>해결</dt>
<dd>YOLOv8 Pose 모델로 랜드마크 추출 파이프라인을 재구성. 가려짐 상황에서도 관절 추적이 안정적으로 유지되었고, 추출 데이터의 누락이 줄어 품질이 향상되면서 최종 모델의 유사도 측정 정확도도 개선됨.</dd>
<dt>배운 점</dt>
<dd>데이터 수집 단계에서의 도구 선택이 최종 모델 성능에 직접적인 영향을 미침을 경험. 분석이 어려운 데이터를 다루는 환경에서는 단순히 사용이 편리한 도구보다, 목표 환경에서의 안정성과 강건성을 우선 검증하고 선택하는 것이 중요함을 배움.</dd>
</dl>
</div>
