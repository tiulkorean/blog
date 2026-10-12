# Tiul Korean (Hugo 블로그)

외부 테마 없이 `layouts/`에 직접 만든 가벼운 테마를 쓰는 Hugo 블로그입니다.
Airflow가 `content/posts/`에 Markdown 파일을 넣으면 그대로 글이 되도록 구성했습니다.

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
hugo.toml              사이트 설정 (제목, 주소, 메뉴, 주소 형식)
archetypes/posts.md    새 글 템플릿 (front matter 규격)
content/
  posts/               ← 블로그 글. Airflow가 파일을 넣을 곳
  about.md             소개 페이지
layouts/               HTML 템플릿 (홈, 목록, 글, 태그/카테고리)
assets/css/main.css    스타일 (색은 맨 위 :root 변수에서 변경)
static/                파비콘 등 그대로 복사되는 파일
netlify.toml           Netlify 배포 설정
```

## 3. 글 파일 규격 (Airflow가 맞춰야 할 형식)

파일명: `content/posts/YYYY-MM-DD-<slug>.md`

```yaml
---
title: "글 제목"
date: 2026-10-12T09:00:00+09:00
slug: "url-slug"                 # 영문·숫자·하이픈. 주소: /posts/2026/10/url-slug/
description: "목록과 검색 결과에 보일 한 줄 요약"
categories: ["표현"]             # 하나만 권장
tags: ["어휘", "문화"]
source:                          # 출처 (없으면 name 을 비워 두면 표시 안 됨)
  name: "국립국어원 표준국어대사전"
  url: "https://stdict.korean.go.kr/"
draft: true                      # 검수 전 true → 확인 후 false 로 바꾸면 공개
---

본문 (Markdown)
```

- `draft: true` 인 글은 `hugo server -D`에서만 보이고 배포 빌드에는 빠집니다. 화면에 **초안** 배지가 붙습니다.
- `date`가 미래인 글도 배포 빌드에서 빠집니다 → 예약 발행처럼 쓸 수 있습니다.
- 같은 `slug`로 파일을 덮어쓰면 같은 주소의 글이 갱신됩니다 (재실행해도 중복 글이 안 생김).

손으로 새 글을 만들 때: `hugo new content posts/2026-10-13-my-post.md`

## 4. 배포 전에 할 일

1. GitHub에 새 저장소를 만들고 이 폴더를 push
2. Netlify(또는 Cloudflare Pages)에서 저장소 연결 → `netlify.toml` 설정이 자동 적용
3. 받은 도메인으로 `hugo.toml`의 `baseURL` 수정
4. `hugo.toml`의 `title`, `params.description` 을 블로그 주제에 맞게 수정

이후 `content/posts/`에 파일이 push 될 때마다 자동으로 빌드·배포됩니다.
