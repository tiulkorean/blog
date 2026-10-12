---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
slug: "{{ .File.ContentBaseName }}"
description: ""
categories: []
tags: []
# 출처 (공공데이터·API 등). 없으면 비워 두세요.
source:
  name: ""
  url: ""
# true 인 동안은 실제 사이트에 나오지 않습니다 (hugo server -D 로만 확인)
draft: true
---

본문을 여기에 작성합니다.
