# ManticoreXL.github.io

최민석(Minseok Choi)의 임베디드 · 로봇 · 시스템 소프트웨어 포트폴리오 사이트.
[Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) Jekyll 테마(remote theme) 기반.

## 로컬 미리보기

```bash
bundle install
bundle exec jekyll serve
# http://127.0.0.1:4000 접속
```

## GitHub Pages 배포

1. 이 레포(`ManticoreXL.github.io`)에 파일을 커밋·푸시합니다.
2. GitHub → **Settings → Pages → Build and deployment**
   - Source: **Deploy from a branch**
   - Branch: **main** / **/(root)**
3. 수 분 뒤 `https://ManticoreXL.github.io` 에서 확인할 수 있습니다.

## 구조

```
.
├── _config.yml              # 사이트 설정 (theme / collection / author)
├── _data/navigation.yml     # 상단 네비게이션
├── _includes/
│   ├── head/custom.html     # 웹폰트 로드
│   └── proj-meta.html       # 프로젝트 메타데이터 스트립
├── _pages/about.md          # About 페이지
├── _portfolio/              # 프로젝트 상세 (4건)
│   ├── vicpinky.md
│   ├── stm32-rccar.md
│   ├── ai-pitching.md
│   └── plc-fifo.md
├── assets/
│   ├── css/main.scss        # 디자인 커스터마이징
│   └── images/              # 프로젝트 스크린샷(추가 예정)
└── index.md                 # 홈 (쇼케이스)
```

## 콘텐츠 수정 가이드

- **프로젝트 추가** — `_portfolio/`에 `.md` 파일을 만들고 front matter(`title`, `excerpt`, `date`, `domain`, `accent`, `period`, `kind`, `role`, `repo`, `stack`)를 채우면 홈 그리드에 자동 반영됩니다.
- **프로필 사진** — `assets/images/avatar.jpg`를 넣고 `_config.yml`의 `author.avatar` 주석을 해제하세요.
- **프로젝트 이미지** — 각 프로젝트 front matter에 `header.teaser` / `header.overlay_image`를 추가하면 썸네일·배너로 사용됩니다.
