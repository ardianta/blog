---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: {{ .BaseFileName }}
date: {{ .Date }}
draft: true

type: page

image: ""
description: ""

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/{{ .Name }}/
---