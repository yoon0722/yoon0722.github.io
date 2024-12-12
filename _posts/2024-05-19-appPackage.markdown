---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "AppPackage, AppActivity 확인하는 명령어"
date: "2024-05-17 00:00:00 +0900"
last_modified_at: "2024-05-17 00:00:00 +0900"
categories:
  - Project
tags:
  - phishinWebView
  - appium
  - linux
author_profile: true
sidebar:
    nav: docs
---

## 현재 실행중인 앱의 AppPackage, AppActivity 확인하는 명령어
```c++
adb shell dumpsys window | find "mCurrentFocus"
```
