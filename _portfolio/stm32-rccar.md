---
title: "STM32 RC카 레이싱 시스템"
excerpt: "Cortex-M4 베어메탈 환경에서 CMSIS로 하드웨어를 직접 제어하고, 블루투스 무선 조종과 센서 기반 출발·결승 판정을 통합한 종합 레이싱 시스템."
date: 2026-04-14
domain: "Embedded · Firmware"
accent: "#0f7a63"
period: "2026.04.03 – 2026.04.14"
kind: "팀 프로젝트 (4인)"
role: "컨트롤러 · RC카 펌웨어 개발, 레포지토리 관리"
repo: "https://github.com/ManticoreXL/STM32_RCCAR_CONTROLLER"
stack:
  - C
  - STM32F411RE
  - CMSIS
  - UART · I2C · SPI
  - PWM · ADC
  - Bluetooth (HC-05)
stack_colors:
  - lang
  - hw
  - hw
  - hw
  - hw
  - tool
header:
  overlay_color: "#0c2545"
  overlay_image: /assets/images/stm32-rccar/cover.jpg
  overlay_filter: "0.45"
  teaser: /assets/images/stm32-rccar/cover.jpg
tags:
  - Embedded
  - STM32
  - Bare-metal
  - Firmware
---

{% include proj-meta.html %}

## 한눈에 보기

> Cortex-M4 베어메탈 환경에서 **CMSIS 레지스터 직접 제어**만으로 모터 구동·무선 통신·센서 판정을 통합한 RC카 레이싱 시스템입니다. 컨트롤러와 RC카 두 모듈의 펌웨어를 담당했습니다.

<div class="facts">
  <div class="fact">
    <span class="fact__k">제어 방식</span>
    <span class="fact__v">CMSIS 레지스터 직접 제어<br><small>HAL 없이 베어메탈로 구현</small></span>
  </div>
  <div class="fact">
    <span class="fact__k">통신 방식</span>
    <span class="fact__v">Bluetooth 2.0 무선통신<br><small>HC-05 블루투스 모듈 -> UART</small></span>
  </div>
</div>

## 배경 & 목표

CORTEX-M4 기반 임베디드 시스템 제어 수업의 최종 프로젝트로, 수업에서 학습한 하드웨어 자원을
**하나의 시스템으로 통합**하는 것을 목표로 삼았습니다. 단순 동작 확인을 넘어 모터 제어와 무선 통신을
결합한 실사용 시나리오를 만들기 위해, 두 대의 RC카가 실제로 겨루는 **레이싱 시스템**을 주제로 선정했습니다.

- **문제** — UART·I2C·SPI·PWM·ADC 등 개별로 학습한 주변장치를, 서로 간섭 없이 하나의 실시간 시스템으로 묶어야 했습니다.
- **목표** — 무선 조종 RC카 + 공정한 출발·결승 판정까지 포함하는, 4개 모듈이 유기적으로 동작하는 레이싱 시스템 구현.

## 시스템 구성

시스템은 **컨트롤러 · RC카 · 스타터 · 피니셔** 4개의 모듈로 구성되며, 모든 모듈이 STM32F411RE(Cortex-M4)
위에서 CMSIS 레지스터 직접 제어로 동작합니다.

![STM32 RC카 시스템 아키텍처](/assets/images/stm32-rccar/architecture.png)
*그림 1. 모듈 구성 및 통신 흐름 — 컨트롤러가 블루투스로 RC카를 조종하고, 스타터·피니셔가 레이스를 통제합니다.*

![전체 시스템 실물 구성](/assets/images/stm32-rccar/system.jpg)
*그림 2. 실물 구성 — 좌우 두 대의 RC카와 컨트롤러, 상단의 스타터·피니셔 도트 매트릭스*

| 모듈 | 핵심 하드웨어 | 주요 인터페이스 |
| --- | --- | --- |
| 컨트롤러 | 아날로그 조이스틱 · 1602 LCD · HC-05 | ADC · I2C · UART |
| RC카 | L298N · DC 모터 · HC-05 | PWM · UART 인터럽트 |
| 스타터 | 조도 센서 · 부저 · MAX7219 | ADC · SPI |
| 피니셔 | 초음파 센서 ×2 · MAX7219 | SPI |

## 담당 구현 (컨트롤러 · RC카)

레이싱 시스템에서 **조작 계통에 해당하는 컨트롤러와 RC카 펌웨어**를 맡아, 무선 통신과 모터 제어를 직접 구현했습니다.

### 컨트롤러 — 명령 송신

![컨트롤러 모듈](/assets/images/stm32-rccar/controller.jpg)
*그림 3. 조이스틱과 1602 LCD를 탑재한 컨트롤러*

- **무엇을** — 전원 인가 시 블루투스로 RC카를 자동 탐색·페어링하고, 조이스틱 입력을 명령으로 변환해 송신합니다.
- **어떻게** — 사전에 AT 모드로 설정한 RC카 주소로 페어링을 반복 시도하고, 완료되면 `RC CONTROLLER` 모드로 전환합니다. 조이스틱 X/Y축 값은 ADC로 읽어 **값이 실제로 변할 때만** 디지털 명령으로 전송합니다.
- **왜** — 매 주기마다 명령을 전송하면 수신측 버퍼가 누적되어 지연이 쌓입니다. 상태 변화가 있을 때만 보내는 **이벤트 기반 송신**으로 불필요한 트래픽을 줄였습니다.

### RC카 — 명령 수신 · 모터 구동

![RC카 내부 회로](/assets/images/stm32-rccar/rccar_internal.jpg)
*그림 4. RC카 내부 — STM32 보드, L298N 모터 드라이버, HC-05, 배터리 배선*

- **무엇을** — 컨트롤러의 방향·속도 명령을 수신해 양측 모터를 독립적으로 구동합니다.
- **어떻게** — **UART 인터럽트**로 제어 명령을 수신하고, 좌우 모터에 서로 다른 **PWM 듀티비**를 인가합니다. 전·후진뿐 아니라 대각선 주행과 제자리 좌·우 회전까지 지원합니다.
- **왜** — 폴링 대신 인터럽트로 수신해 메인 루프가 모터 제어에 집중하도록 했고, 듀티비를 분리 제어해 부드러운 방향 전환을 구현했습니다.

## 전체 시스템 동작 (스타터 · 피니셔)

스타터·피니셔 모듈은 팀원이 담당했으며, 제가 만든 컨트롤러·RC카와 결합되어 하나의 레이스로 동작합니다.

- **스타터** — 조도 센서로 두 차량의 대기 상태를 확인하고, 버튼에서 손을 떼면 부저·도트 매트릭스로 카운트다운을 시작합니다. 카운트다운이 끝나기 전 이탈하면 **부정 출발**로 판정합니다.
- **피니셔** — 결승선 양쪽 레인의 초음파 센서로 진입 차량을 스캔해, 먼저 통과한 차량을 **밀리초 단위**로 판정합니다.

<video src="/assets/images/stm32-rccar/false_start.mp4" autoplay muted loop playsinline width="100%" style="border-radius:12px; border:1px solid #e3e8ee;"></video>
*부정 출발 감지 — 카운트다운 종료 전 이탈한 차량을 도트 매트릭스에 즉시 표시*

## 트러블슈팅

<div class="ts" markdown="1">
<div class="ts__head"><span class="ts__tag">Trouble 01</span>모터 드라이버 역기전력으로 인한 통신 끊김</div>
<dl>
<dt>문제</dt>
<dd>RC카 주행 중 블루투스 모듈의 설정값이 초기화되어, RC카와 컨트롤러 간 연결이 끊기는 증상이 발생했습니다. 특히 급가속·급제동 구간에서 두드러졌습니다.</dd>
<dt>원인</dt>
<dd>펌웨어와 AT 모드 설정값만 반복해서 점검하다 해결되지 않아, 한 발 물러서 하드웨어 범위까지 시야를 넓혔습니다. 그 결과 모터 회전이 멈출 때 L298N 모터 드라이버에서 발생하는 역기전력이 회로에 과부하를 주고, AT 모드로 설정한 HC-05의 설정값을 초기화시킨다는 것을 확인했습니다.</dd>
<dt>해결</dt>
<dd>HC-05 결선부와 모터 드라이버 결선부를 물리적으로 분리해 역기전력의 영향을 차단했습니다. 이후 주행에서 블루투스 연결 끊김이 해소되었습니다.</dd>
<dt>배운 점</dt>
<dd>임베디드 시스템에서는 소프트웨어뿐 아니라 하드웨어 회로 수준의 영향까지 함께 고려해야 함을 체득했습니다. 증상의 원인을 특정 범위로 한정하지 않고, 좁혀진 시야를 의식적으로 다시 넓히는 디버깅 태도의 중요성을 알게 됐습니다.</dd>
</dl>
</div>

<div class="ts" markdown="1">
<div class="ts__head"><span class="ts__tag">Trouble 02</span>UART 버퍼 오버플로우로 인한 조작 지연 누적</div>
<dl>
<dt>문제</dt>
<dd>연결 후 시간이 지날수록 조이스틱 입력부터 RC카의 명령 수행까지 지연이 점점 늘어나, 실시간 조작성이 떨어지는 증상이 발생했습니다.</dd>
<dt>원인</dt>
<dd>RC카는 UART 인터럽트로 제어 패킷을 수신하는데, 버퍼에서 패킷이 처리되는 속도보다 더 빠르게 패킷이 들어와 시간이 지날수록 레이턴시가 누적됐습니다.</dd>
<dt>해결</dt>
<dd>중복 제어 패킷 전송을 크게 줄이고, 조이스틱 값이 확실하게 변할 때만 패킷을 전송하도록 변경해 버퍼 오버플로우를 예방했습니다. 그 결과 조작 지연이 2~3초 대에서 실시간 수준까지 감소했습니다.</dd>
<dt>배운 점</dt>
<dd>실시간 시스템에서는 송신측과 수신측의 처리 속도를 함께 고려해야 함을 체득했습니다. 데이터를 자주 보내는 것이 곧 신뢰성을 의미하지는 않으며, 실질적인 상태 변화가 있을 때만 신호를 보내는 이벤트 기반 설계가 임베디드 통신 환경에서 더 효율적이고 안정적임을 알게 됐습니다.</dd>
</dl>
</div>

## 결과 및 시연

두 대의 RC카가 무선 조종으로 출발 통제부터 결승 판정까지 완주하는, 통합 레이싱 시스템을 완성했습니다.

<video src="/assets/images/stm32-rccar/racing.mp4" controls muted loop playsinline width="100%" style="border-radius:12px; border:1px solid #e3e8ee;"></video>
*레이싱 주행 시연*

![완성된 RC카](/assets/images/stm32-rccar/rccar_done.jpg)
*그림 5. 커버까지 장착해 완성한 두 대의 RC카*

## 회고

- **잘된 점** — 개별로 학습한 주변장치(UART·I2C·SPI·PWM·ADC)를 간섭 없이 하나의 실시간 시스템으로 통합했고, 베어메탈 환경에서 무선 통신의 안정성을 직접 끌어올린 경험을 얻었습니다.
- **아쉬운 점 / 개선 방향** — 제어 패킷에 별도의 검증·재전송 절차가 없어, 향후에는 체크섬과 ACK 기반의 경량 프로토콜을 더해 통신 신뢰성을 한층 높이고 싶습니다.