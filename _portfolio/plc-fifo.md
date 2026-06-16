---
title: "PLC 선입선출(FIFO) 적재 시스템"
excerpt: "MELSEC-Q PLC와 MPS 훈련 장비로 소재의 가공·분류·적재·하역을 자동화하고, 우선순위 관리와 선입선출 알고리즘을 HMI로 제어하는 지능형 공정 라인."
date: 2026-02-09
domain: "Industrial · PLC"
accent: "#b26a00"
period: "2026.02.05 – 2026.02.09"
kind: "팀 프로젝트"
role: "프로젝트 기획·관리, PLC 시퀀스 설계, HMI 작화"
repo: "https://github.com/ManticoreXL/PLC-Programming"
stack:
  - PLC (MELSEC-Q)
  - Ladder
  - HMI (GOT2000)
  - GX Works2
  - GT Designer3
  - MPS
header:
  overlay_color: "#0c2545"
  overlay_filter: "0.15"
tags:
  - PLC
  - Industrial Automation
  - HMI
  - Sequence Control
---

{% include proj-meta.html %}

## 프로젝트 개요

**MPS 훈련 장비**를 최대한 활용하여 지능화된 공정 라인을 구상한 프로젝트입니다.
소재의 가공·분류·적재·하역 과정을 자동화하고, 각 창고별 **우선순위 관리와 선입선출(FIFO)**을 적용해
유연한 적재 알고리즘을 구현했으며, 전체 공정을 **HMI**로 모니터링·제어할 수 있도록 인터페이스를 작화했습니다.

## 시스템 구성

- **MITSUBISHI PLC Q03UDVCPU (MELSEC-Q)** — 제어 컨트롤러
- **GOT2000 HMI Device** — 모니터링 / 제어 인터페이스
- **MPS 훈련 장비** — 가공·분류·적재 대상 공정 라인

> 개발 환경: GX Works 2 (1.631H) · GT Designer 3 (1.256S) · GT Simulator 3 (1.256S)

## 핵심 구현 — PLC 시퀀스 설계

- 투입된 소재를 가공한 뒤 센서로 **재질을 판별**하고 컨베이어 벨트로 끝까지 이동
- 서보 모터와 흡착 실린더로 적재 창고에 적재하고, **데이터 레지스터에 우선순위를 기록**
- 창고에서 특정 소재만 **선택적으로 하역**하거나 **일괄 하역**할 수 있는 알고리즘 설계
- 특정 소재의 창고가 모두 가득 찬 상태에서 신규 소재가 투입되면 **선입선출 순서로 하역 및 적재**

순차적 장비 점검, 선입선출 적재·하역, 우선순위 관리, 시청각적 피드백 기능을 함께 구현하고
HMI 작화로 자동화 공정을 편리하게 제어·관리할 수 있도록 구성했습니다.

## 시연 영상

전체 시연 영상입니다.

{% include video id="sFaWmrRSi6g" provider="youtube" %}

세부 시연:

- **순차적 장비 점검** — <https://www.youtube.com/watch?v=1OP95QDDXJI>
- **소재 가공 및 FIFO 적재** — <https://www.youtube.com/watch?v=opKqtnrGvCA>
- **소재 개별 하역 및 일괄 하역** — <https://www.youtube.com/watch?v=EgyRwv3C1IU>
