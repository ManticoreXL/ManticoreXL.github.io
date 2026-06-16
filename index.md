---
layout: splash
permalink: /
title: "Minseok Choi — Embedded & Robotics Engineer"
classes:
  - landing
---

<header class="hero">
  <div class="hero__eyebrow">EMBEDDED SYSTEMS<span class="dot">·</span>ROBOTICS</div>
  <h1 class="hero__title">
    최민석
    <span class="en">Minseok Choi</span>
  </h1>
  <p class="hero__role">임베디드 시스템 · 로봇 소프트웨어 엔지니어 (직무 희망)</p>
  <p class="hero__desc">
    하드웨어와 소프트웨어의 경계에서 동작하는 시스템을 설계하고 구현합니다. <br>
    임베디드 시스템과 운영체제, 하드웨어 제어에 관심이 있습니다.
  </p>

  <div class="hero__actions">
    <a class="hero__btn hero__btn--solid" href="#projects">프로젝트 보기 ↓</a>
    <a class="hero__btn hero__btn--ghost" href="https://github.com/ManticoreXL" target="_blank" rel="noopener">
      <i class="fab fa-github" aria-hidden="true"></i> GitHub
    </a>
    <a class="hero__btn hero__btn--ghost" href="mailto:zip3366@naver.com">
      <i class="fas fa-envelope" aria-hidden="true"></i> Email
    </a>
  </div>

  <div class="hero__spec">
    Kwangwoon Univ. — Computer Engineering <span class="sep">/</span>C · C++ · Python<span class="sep">/</span>Linux · STM32 · ROS2
  </div>
</header>

<section class="section" id="about">
  <span class="section__eyebrow">// about</span>
  <h2 class="section__title">소개</h2>
  <div class="facts">
    <div class="fact">
      <span class="fact__k">Education</span>
      <span class="fact__v">광운대학교 컴퓨터정보공학부<br><small>2020.03 – 2026.02</small></span>
    </div>
    <div class="fact">
      <span class="fact__k">Training</span>
      <span class="fact__v">AI 융합 로봇 SW 개발자 과정<br><small>대한상공회의소 서울기술교육센터<br>25.12.23 ~ 26.07.21</small></span>
    </div>
  </div> <br>

  <p>
    광운대학교 컴퓨터정보공학부를 졸업하고, 현재 대한상공회의소 서울기술교육센터에서
    <strong>AI 융합 로봇 SW 개발자 과정</strong>을 진행 중에 있습니다. <br> 
    Linux 및 MCU 기반의 펌웨어 개발부터 ROS2, 컴퓨터비전 등 임베디드 시스템 및 로봇 제어 분야에서 다수의 팀 프로젝트를 수행했습니다. <br>
    트러블슈팅에서 하드웨어 레벨과 소프트웨어 아키텍처를 통합적으로 분석하는, 넓은 관점에서의 접근법을 지향합니다.
  </p>
</section>

<section class="section" id="projects">
  <span class="section__eyebrow">// projects</span>
  <h2 class="section__title">프로젝트</h2>

  <div class="proj-list"> {% assign items = site.portfolio | sort: "date" | reverse %}
    {% for p in items %}
    <a class="proj-card--large" href="{{ p.url | relative_url }}" style="--accent: {{ p.accent | default: '#0d4fbd' }}">
      <div class="proj-card__content">
        <span class="proj-card__eyebrow">{{ p.domain }}</span>
        <h3 class="proj-card__title">{{ p.title }}</h3>
        <p class="proj-card__summary">{{ p.excerpt }}</p>
        
        <div class="proj-card__stack">
          {% for s in p.stack %}
            {% assign c = p.stack_colors[forloop.index0] | default: "" %}
            <span class="chip{% if c != "" %} chip--{{ c }}{% endif %}">{{ s }}</span>
          {% endfor %}
        </div>
        
        <span class="proj-card__link">프로젝트 상세 내용 및 기술 문서 보기 →</span>
      </div>
    </a>
    {% endfor %}
  </div>
</section>

<section class="section">
  <div class="contact-strip">
    <h2> 제 역량을 발휘할 기회를 찾고 있습니다</h2>
    <p>임베디드 시스템 · OS · 로봇 소프트웨어 분야의 직무를 희망합니다.</p>
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
