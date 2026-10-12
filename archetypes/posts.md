---
# ── 기본 ───────────────────────────────
title: "English title of the lesson"
date: {{ .Date }}
slug: "{{ .File.ContentBaseName }}"
description: "One-line English summary shown in lists and search results."

# ── 오늘의 핵심 표현 (글 상단에 크게 표시) ──
expression:
  ko: "한국어 표현"
  roman: "hangugeo pyohyeon"
  en: "English meaning"

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
