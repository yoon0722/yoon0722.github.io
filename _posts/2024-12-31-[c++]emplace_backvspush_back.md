---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] emplace_back vs push_back"
date: "2024-12-31 00:00:00 +0900"
last_modified_at: "2024-12-31 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

## emplace_back
- push_back과 유사하게 새로운 요소를 컨테이너(vector, deque)의 끝에 추가하는 기능.
- 새로운 객체를 직접 생성하여 삽입할 수 있다는 점에서 push_back과 차이가 있다.

## emplace_back vs push_back
### push_back
- 복사 또는 이동을 통해 객체를 삽입
- 이미 존재하는 객체를 컨테이너에 넣을 때 사용된다.
```c++
vector<int> vec;
int x = 5;
vec.push_back(x); //x를 복사하여 vec에 추가
```

### emplace_back
- 객체를 직접 생성하여 컨테이너 끝에 추가
```c++
vector<pair<int, int>> vec;
vec.emplace_back(1, 2); //(1,2)값을 가진 pair 객체를 직접 생성하여 vec에 추가
```

## emplace_back의 장점
- 객체를 바로 생성하므로 불필요한 복사나 이동이 일어나지 않는다.
  - 특히 복잡한 객체나 큰 객체를 다룰 때 성능차이가 난다.
- 객체의 생성자를 직접 호출할 수 있기 때문에, 객체를 미리 생성하고 넣는것보다 더 간단하게 요소를 추가할 수 있다.