---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "브루트 포스(Brute Force) 알고리즘"
date: "2024-06-27 00:00:00 +0900"
last_modified_at: "2024-06-27 00:00:00 +0900"
categories:
  - Algorithm
tags:
author_profile: true
sidebar:
    nav: docs
---

## 완전탐색, 브루트 포스(Brute Force) 알고리즘
**Brute: 단순한, 무식한** 
<br/> **Force: 힘**
- 가능한 모든 경우의 수를 다 검사해보는 방식의 알고리즘
- 문제를 해결하는 가장 직관적이고 단순한 방법 중 하나이다.

### Brute Force Attack
- 비밀번호의 모든 조합을 다 시도해보는 방법
<br/>ex) 3자리수의 비밀번호를 풀기 위해 000~999까지 모든 경우의 수를 전부 입력해본다.

### 장점
- 구현이 매우 간단하며 직관적이다.
- 가능한 모든 경우의 수를 다 시도하므로, 항상 정확한 결과를 도출할 수 있다.

### 단점
- 입력의 크기가 커지면 실행 시간이 급격히 증가한다.
- 시간 복잡도가 매우 높다.

### 브루트 포스(Brute Force) 구현 방법
1. for/while loop
2. 재귀함수