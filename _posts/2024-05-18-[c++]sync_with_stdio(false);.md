---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] ios::sync_with_stdio(false) 성능향상 및 시간초과해결"
date: "2024-05-20 00:00:00 +0900"
last_modified_at: "2024-05-20 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

```c++
ios::sync_with_stdio(false);
cin.tie(NULL);
cout.tie(NULL);
```

## ios::sync_with_stdio(false);
- C++의 표준 입출력 버퍼를 C 표준 입출력 버퍼와 동기화하지 않도록 설정한다.

기본적으로 C++ 표준 입출력은 C 표준 입출력 버퍼와 동기화되어 있어 C++의 'cin'과 'cout'을 사용할 때마다 C 표준 입출력 버퍼와 동기화되는 오버헤드가 발생한다.
<br/>ex) C의 'printf, scanf'와 C++의 'cin ,cout' 같이 사용가능.
<br/>**따라서 대량의 입출력이 필요한 경우에는 이 동기화를 끄고, C++의 입출력만을 사용하면 성능을 향상시킬 수 있다.**

## cin.tie(NULL);
- 'cin'과 'cout'이 묶여있는것을 풀어주는 역할을 한다.

'cin.tie(NULL);'을 호출하면 'cin'과 'cout'이 묶여있는것을 풀어줘서 'cin'으로 입력을 받을 때 자동으로 'cout'의 버퍼를 비우지 않도록 설정한다.

## cout.tie(NULL);
- 'cout'의 버퍼를 비우지 않도록 설정하여 출력이 즉시 이루어지도록 한다.

기본적으로 'cout'의 출력은 버퍼링되어 출력이 일어날때마다 버퍼에 쌓이다가 특정 조건이 만족되면 출력된다.
