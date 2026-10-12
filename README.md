# Tiul Korean (Hugo 블로그)

외국인 한국어 학습자를 위한 블로그입니다. 화면·설명은 영어, 학습 대상인 한국어는 로마자·번역과 함께 보여 줍니다.
외부 테마 없이 `layouts/`에 직접 만든 테마를 쓰며, Airflow가 `content/posts/`에 Markdown 파일을 넣으면 그대로 글이 됩니다.

## 1. 로컬에서 실행

[Hugo extended](https://gohugo.io/installation/) 0.146 이상이 필요합니다 (개발은 0.167.0 기준).

```bash
# macOS
brew install hugo
# Windows
winget install Hugo.Hugo.Extended

hugo server -D        # http://localhost:1313  (-D: 초안까지 보기)
hugo --gc --minify    # 배포용 빌드 → public/
```

## 2. 폴더 구조

```
hugo.toml                  사이트 설정 (제목, 메뉴, 주소 형식, 난이도 이름)
archetypes/posts.md        새 글 템플릿 = 글 파일 규격
content/
  posts/                   ← 레슨 글. Airflow가 파일을 넣을 곳
  levels/                  난이도별 소개 문구 (beginner / intermediate / advanced)
  about.md                 소개 페이지
layouts/
  page.html                글 화면 (핵심 표현 → 본문 → 예문 → 단어장 → 퀴즈)
  _partials/lesson-blocks.html   예문·단어장·퀴즈 렌더링
assets/css/main.css        스타일 (색은 :root 변수에서 변경)
netlify.toml               Netlify 배포 설정 (다른 곳에 배포하면 무시해도 됨)
```

## 3. 글 파일 규격 (Airflow가 맞춰야 할 형식)

파일명: `content/posts/YYYY-MM-DD-<slug>.md`

```yaml
---
title: "English title of the lesson"            # 필수
date: 2026-10-12T09:00:00+09:00                  # 필수 (KST)
slug: "nunchi"                                   # 필수. 영문 소문자·숫자·하이픈
description: "One-line English summary."         # 목록·검색 결과에 표시

expression:                     # 오늘의 핵심 표현 (글 상단 강조 박스)
  ko: "눈치"
  roman: "nunchi"               # 국립국어원 로마자 표기법 기준 권장
  en: "the ability to sense the mood"

levels: ["intermediate"]        # beginner | intermediate | advanced 중 하나
categories: ["Expressions"]     # Expressions | Grammar | Culture | Vocabulary ...
tags: ["culture"]

vocab:                          # 단어장 카드
  - { ko: "눈치", roman: "nunchi", en: "social awareness" }
examples:                       # 예문 (ko/en 에 **굵게** 같은 Markdown 사용 가능)
  - ko: "걔는 진짜 **눈치가 없어**."
    roman: "gyaeneun jinjja nunchiga eopseo."
    en: "He really can’t read the room."
quiz:                           # 객관식 퀴즈 (클릭하면 정답·해설 표시)
  - question: "Which phrase means ...?"
    options: ["눈치가 빠르다", "눈치가 없다"]
    answer: 1                   # 정답 options 의 순서 (0부터 시작)
    explanation: "Why it’s the answer."

source:                         # 출처. 없으면 name 을 비워 두면 표시 안 됨
  name: "National Institute of Korean Language — Standard Korean Dictionary"
  url: "https://stdict.korean.go.kr/"

draft: true                     # 검수 전 true → 확인 후 false 로 바꾸면 공개
---

English explanation in Markdown. Korean can be mixed in, e.g. **눈치** (*nunchi*).
```

규칙
- `expression`, `vocab`, `examples`, `quiz`, `source` 는 선택 항목입니다. 없으면 해당 섹션이 화면에 나오지 않습니다.
- 본문(Markdown)에는 설명만 쓰고, 예문·단어·퀴즈는 위 데이터 필드에 넣으세요. 화면 배치는 템플릿이 통일해 줍니다.
- `draft: true` 인 글은 `hugo server -D`에서만 보이고 배포 빌드에서 빠집니다. 화면에 **Draft** 배지가 붙습니다.
- `date`가 미래인 글도 배포 빌드에서 빠집니다 → 예약 발행처럼 쓸 수 있습니다.
- 같은 `slug`로 파일을 덮어쓰면 같은 주소의 글이 갱신됩니다 (재실행해도 중복 글이 안 생김).
- 주소 형식: 레슨 `/lessons/<slug>/`, 목록 `/lessons/` (파일은 계속 `content/posts/`에 둠)

### 이미지·영상

front matter로 넣기 (Airflow 권장 — 화면 위치가 통일됨)

```yaml
cover:                     # 글 상단 대표 이미지 + 목록 썸네일 + SNS 공유 미리보기(og:image)
  src: "/images/nunchi.jpg"      # static/images/ 에 둔 파일, 또는 https://... 외부 주소
  alt: "People at a meeting table"
  credit: "Photo: Unsplash"
video:                     # 유튜브 영상 (핵심 표현 박스 바로 아래)
  youtube: "VIDEO_ID"      # youtube.com/watch?v=VIDEO_ID
  start: 30                # 시작 초 (선택)
  caption: "How to say 눈치"
```

본문 안에 넣기 (설명 중간에 넣고 싶을 때)

```markdown
![Alt text](/images/example.jpg)

{{</* youtube VIDEO_ID */>}}
```

이미지 파일은 `static/images/`에 두면 `/images/파일명`으로 쓸 수 있습니다.
글마다 이미지가 많으면 글을 폴더로 만들어도 됩니다: `content/posts/2026-10-13-xxx/index.md` + 같은 폴더의 `cover.jpg` → `src: "cover.jpg"`
이미지·영상은 직접 찍었거나 사용이 허락된 것만 쓰세요 (Unsplash 등 무료 라이선스, 공공누리 이미지 등).

손으로 새 글을 만들 때: `hugo new content posts/2026-10-13-my-lesson.md`

## 4. 배포 전에 할 일

1. GitHub에 새 저장소를 만들고 이 폴더를 push
2. 배포 서비스(GitHub Pages / Cloudflare Pages / Netlify)에 저장소 연결
3. 받은 도메인으로 `hugo.toml`의 `baseURL` 수정

이후 `content/posts/`에 파일이 push 될 때마다 자동으로 빌드·배포됩니다.
