# 🌻 SOLSOLHANE Claude Skills Marketplace

Claude Code에서 바로 설치해 사용할 수 있는 **커스텀 스킬(플러그인) 마켓플레이스**입니다.

| 플러그인 | 설명 | 버전 |
|---------|------|------|
| [email-html-compat-plugin](#-email-html-compat-plugin) | 웹 HTML/CSS 코드를 이메일 본문 발송용 HTML로 변환하는 전문 스킬 | 1.0.0 |

---

## 🚀 설치 방법

Claude Code 세션에서 아래 명령어를 순서대로 입력하면 됩니다.

### 1. 마켓플레이스 등록

```
/plugin marketplace add soljjang777/solsolhane-marketplace
```

### 2. 플러그인 설치

```
/plugin install email-html-compat-plugin@solsol-claude-skills
```

또는 `/plugin` 명령어로 플러그인 관리 UI를 열어 **solsol-claude-skills** 마켓플레이스에서 원하는 플러그인을 직접 선택해 설치할 수도 있습니다.

### 3. 설치 확인

```
/plugin
```

설치된 플러그인 목록에 `email-html-compat-plugin`이 보이면 완료입니다. 설치 후에는 별도 호출 없이, 관련 요청을 하면 Claude가 자동으로 스킬을 사용합니다.

---

## 📧 email-html-compat-plugin

웹용 HTML/CSS를 **주요 이메일 클라이언트에서 깨지지 않는 발송용 HTML**로 변환해 주는 스킬입니다.

이메일 클라이언트는 일반 브라우저와 달리 `flex`, `grid`, `<style>` 태그, 외부 CSS 등을 지원하지 않는 경우가 많습니다. 이 스킬은 그런 제약을 모두 반영해 **table 기반 레이아웃 + inline style** 구조로 코드를 재구성합니다.

### 지원 이메일 클라이언트

- **Gmail 웹** (Chrome/Firefox)
- **Gmail 앱** (Android/iOS)
- **Apple Mail** (macOS/iOS)
- **Outlook Windows** (2016/2019/2021/365 — Word 렌더링 엔진)
- **Outlook Web (OWA)**
- **Samsung Email** (Android)

### 주요 기능

- `div + flex/grid` 레이아웃 → `table > tr > td` 구조로 자동 재구성
- 모든 CSS를 **inline style**로 이식 (Gmail 앱 대응)
- Outlook 호환을 위한 **VML bulletproof 버튼**, 조건부 주석(`<!--[if mso]>`) 자동 적용
- 이메일에서 깨지는 속성(`position`, `float`, `calc()`, `transform` 등) 제거 및 안전한 대체
- 이미지·폰트·간격(margin → padding/spacer) 이메일 호환 방식으로 교체
- 100% wrapper + 600px 컨테이너의 표준 이메일 구조 적용
- 출력 전 자체 검증 체크리스트로 호환성 점검

### 사용 방법

설치 후 Claude Code에서 아래와 같은 키워드로 요청하면 스킬이 자동으로 동작합니다.

> - "이 코드를 **이메일 HTML로 변환**해줘"
> - "**이메일 발송용 HTML**로 만들어줘"
> - "**뉴스레터 코드**로 바꿔줘"
> - "**Outlook 호환**되게 수정해줘"
> - "**이메일 템플릿 변환**해줘"

#### 사용 예시

```
이 HTML을 이메일 발송용으로 변환해줘

<div style="display:flex; gap:16px;">
  <div class="card">상품 A</div>
  <div class="card">상품 B</div>
</div>
```

변환이 완료되면 아래 형식으로 결과를 출력합니다.

1. **최종 이메일용 HTML** — 본문에 바로 붙여넣어 발송 가능한 완성형 전체 코드
2. **변경한 핵심 포인트** — 무엇을 어떻게 바꿨는지 요약
3. **클라이언트별 주의사항** — Outlook, Gmail 앱 등에서 주의할 점

---

## 📂 저장소 구조

```
solsolhane-marketplace/
├── .claude-plugin/
│   └── marketplace.json                  # 마켓플레이스 정의
├── plugins/
│   └── email-html-compat-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json               # 플러그인 메타데이터
│       └── skills/
│           └── email-html-compat/
│               └── SKILL.md              # 스킬 본문 (변환 규칙/프로세스)
└── README.md
```

---

## 🔄 업데이트 / 제거

```
# 마켓플레이스 최신 버전 반영
/plugin marketplace update solsol-claude-skills

# 플러그인 제거
/plugin uninstall email-html-compat-plugin@solsol-claude-skills
```

---

## 🤝 기여

새로운 스킬 추가나 개선 제안은 [Issues](https://github.com/soljjang777/solsolhane-marketplace/issues) 또는 Pull Request로 환영합니다.

새 플러그인을 추가하려면:

1. `plugins/<플러그인-이름>/` 디렉터리를 만들고 `.claude-plugin/plugin.json`과 `skills/<스킬-이름>/SKILL.md`를 작성
2. 루트의 `.claude-plugin/marketplace.json`의 `plugins` 배열에 항목 추가

---

## 📜 라이선스 / 소유자

- Owner: **SOLSOLHANE**
