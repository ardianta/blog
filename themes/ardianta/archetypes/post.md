---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: {{ .BaseFileName }}
date: {{ .Date }}
draft: true

type: post

tags:
    - tag

image: ""
description: ""

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/{{ .Name }}/
---