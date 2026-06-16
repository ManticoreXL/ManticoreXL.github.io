---
layout: splash
permalink: /
title: "Minseok Choi — Embedded & Robotics Engineer"
classes:
  - landing
---

<header class="hero">
  <div class="hero__eyebrow">EMBEDDED<span class="dot">·</span>ROBOTICS<span class="dot">·</span>SYSTEMS</div>
  <h1 class="hero__title">
    최민석
    <span class="en">Minseok Choi</span>
  </h1>
  <p class="hero__role">임베디드 시스템 · 로봇 소프트웨어 엔지니어</p>
  <p class="hero__desc">
    베어메탈 펌웨어부터 ROS2 기반 로봇 시스템, 산업 자동화 공정까지 —
    하드웨어와 소프트웨어의 경계에서 동작하는 시스템을 설계하고 구현합니다.
    레지스터 수준의 제어와 실시간 통신, 그리고 그 위에 올라가는 통합 시스템에 관심이 많습니다.
  </p>

  <div class="hero__actions">
    <a class="hero__btn hero__btn--solid" href="#projects">프로젝트 보기 →</a>
    <a class="hero__btn hero__btn--ghost" href="https://github.com/ManticoreXL" target="_blank" rel="noopener">
      <i class="fab fa-github" aria-hidden="true"></i> GitHub
    </a>
    <a class="hero__btn hero__btn--ghost" href="mailto:zip3366@naver.com">
      <i class="fas fa-envelope" aria-hidden="true"></i> Email
    </a>
  </div>

  <div class="hero__spec">
    Kwangwoon Univ. — Computer Engineering<span class="sep">/</span>Seoul, KR<span class="sep">/</span>C · C++ · Python<span class="sep">/</span>STM32 · Linux · ROS2
  </div>
</header>

<section class="section" id="about">
  <span class="section__eyebrow">// about</span>
  <h2 class="section__title">소개</h2>

  <p>
    광운대학교 컴퓨터정보공학부를 졸업하고, 대한상공회의소 서울기술교육센터에서
    <strong>AI SW 융합 로봇 개발자 과정</strong>을 이수했습니다. MCU 펌웨어, Linux 시스템 프로그래밍,
    ROS2 로봇 제어, 컴퓨터비전, PLC 산업 자동화까지 임베디드·로봇 분야를 폭넓게 다뤄 왔으며,
    문제가 생겼을 때 <strong>하드웨어와 소프트웨어를 함께 들여다보는 디버깅</strong>을 중요하게 생각합니다.
  </p>

  <div class="facts">
    <div class="fact">
      <span class="fact__k">Education</span>
      <span class="fact__v">광운대학교 컴퓨터정보공학부<br><small>2020.03 – 2026.02 · GPA 3.52 / 4.50</small></span>
    </div>
    <div class="fact">
      <span class="fact__k">Training</span>
      <span class="fact__v">AI SW 융합 로봇 개발자 과정<br><small>대한상공회의소 서울기술교육센터</small></span>
    </div>
    <div class="fact">
      <span class="fact__k">Training</span>
      <span class="fact__v">NAND/SSD 플래시 기초 및 기술 개요<br><small>광운대학교 반도체기술교육센터</small></span>
    </div>
    <div class="fact">
      <span class="fact__k">Certificate</span>
      <span class="fact__v">TOPCIT 3수준<br><small>IITP · 2025.05</small></span>
    </div>
  </div>
</section>

<section class="section" id="skills">
  <span class="section__eyebrow">// stack</span>
  <h2 class="section__title">기술 스택</h2>

  <div class="skills">
    <div class="skill-group">
      <div class="skill-group__label">Languages</div>
      <div class="skill-group__items">
        <span class="chip">C</span><span class="chip">C++</span><span class="chip">Python</span>
        <span class="chip">JavaScript</span><span class="chip">TypeScript</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group__label">Embedded &amp; HW</div>
      <div class="skill-group__items">
        <span class="chip">STM32 (Cortex-M4)</span><span class="chip">CMSIS</span>
        <span class="chip">Linux Kernel / Module</span><span class="chip">Device Driver</span>
        <span class="chip">UART · I2C · SPI</span><span class="chip">PWM · ADC</span>
        <span class="chip">Raspberry Pi</span><span class="chip">Jetson Nano</span>
        <span class="chip">PLC (MELSEC-Q)</span><span class="chip">HMI</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group__label">Robotics</div>
      <div class="skill-group__items">
        <span class="chip">ROS2 (Jazzy)</span><span class="chip">Nav2</span>
        <span class="chip">SLAM Toolbox</span><span class="chip">Imitation Learning</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group__label">AI · Vision</div>
      <div class="skill-group__items">
        <span class="chip">YOLO / YOLOv8 Pose</span><span class="chip">OpenCV</span>
        <span class="chip">MediaPipe</span><span class="chip">TensorFlow / Keras</span>
      </div>
    </div>
    <div class="skill-group">
      <div class="skill-group__label">Tools · Etc</div>
      <div class="skill-group__items">
        <span class="chip">Git</span><span class="chip">Flask</span><span class="chip">SQLite</span>
        <span class="chip">React</span><span class="chip">Cloudflare</span>
        <span class="chip">GX Works2</span><span class="chip">GT Designer3</span>
      </div>
    </div>
  </div>
</section>

<section class="section" id="projects">
  <span class="section__eyebrow">// projects</span>
  <h2 class="section__title">프로젝트</h2>

  <div class="proj-grid">
    {% assign items = site.portfolio | sort: "date" | reverse %}
    {% for p in items %}
    <a class="proj-card" href="{{ p.url | relative_url }}" style="--accent: {{ p.accent | default: '#0d4fbd' }}">
      <span class="proj-card__eyebrow">{{ p.domain }}</span>
      <h3 class="proj-card__title">{{ p.title }}</h3>
      <p class="proj-card__summary">{{ p.excerpt }}</p>
      <div class="proj-card__stack">
        {% for s in p.stack limit: 5 %}<span class="chip">{{ s }}</span>{% endfor %}
      </div>
      <span class="proj-card__link">자세히 보기 →</span>
    </a>
    {% endfor %}
  </div>
</section>

<section class="section">
  <div class="contact-strip">
    <h2>함께 일할 기회를 찾고 있습니다</h2>
    <p>임베디드 시스템 · OS · 로봇 소프트웨어 분야의 제안을 환영합니다.</p>
    <div class="hero__actions">
      <a class="hero__btn hero__btn--solid" href="mailto:zip3366@naver.com">
        <i class="fas fa-envelope" aria-hidden="true"></i> zip3366@naver.com
      </a>
      <a class="hero__btn hero__btn--ghost" href="https://github.com/ManticoreXL" target="_blank" rel="noopener">
        <i class="fab fa-github" aria-hidden="true"></i> github.com/ManticoreXL
      </a>
    </div>
  </div>
</section>
