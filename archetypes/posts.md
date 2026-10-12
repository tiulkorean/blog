---
# ── 기본 ───────────────────────────────
title: "English title of the lesson"
date: {{ .Date }}
slug: "{{ .File.ContentBaseName | replaceRE `^[0-9]{4}-[0-9]{2}-[0-9]{2}-` `` }}"
description: "One-line English summary shown in lists and search results."

# ── 오늘의 핵심 표현 (글 상단에 크게 표시) ──
expression:
  ko: "한국어 표현"
  roman: "hangugeo pyohyeon"
  en: "English meaning"

# ── 미디어 (선택. 없으면 지우거나 비워 두기) ──
cover:                        # 대표 이미지: 글 상단 + 목록 썸네일 + SNS 공유 미리보기
  src: ""                     # https://... 또는 /images/파일.jpg (static/images 폴더)
  alt: ""                     # 이미지 설명 (영어)
  credit: ""                  # 사진 출처 표기
video:                        # 유튜브 영상 (핵심 표현 박스 아래에 표시)
  youtube: ""                 # 영상 ID (youtube.com/watch?v=<이 부분>)
  start: 0                    # 시작 초 (선택)
  caption: ""

# ── 분류 ───────────────────────────────
levels: ["beginner"]          # beginner | intermediate | advanced 중 하나
categories: ["Expressions"]   # Expressions | Grammar | Culture | Vocabulary ...
tags: []

# ── 학습 데이터 (없으면 섹션이 표시되지 않음) ──
vocab:
  - ko: "단어"
    roman: "daneo"
    en: "word"
examples:
  - ko: "예문입니다."
    roman: "yemunimnida."
    en: "This is an example sentence."
quiz:
  - question: "Question in English?"
    options: ["A", "B", "C"]
    answer: 0                 # 정답 options 의 순서 (0부터)
    explanation: "Why this is the answer."

# ── 출처 (없으면 name 을 비워 두기) ──
source:
  name: ""
  url: ""

draft: true
---

Write the explanation in English here. Use Korean inside the text freely, e.g. **눈치** (*nunchi*).
