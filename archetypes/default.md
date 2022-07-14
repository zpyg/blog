---
title: "{{ replace .Name "-" " " | title }}"
description: ""
date: {{ .Date }}
categories:
  - {{ path.Base .File.Dir }}
tags: []
---

