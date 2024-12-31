---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] stack vs queue vs deque"
date: "2024-12-23 00:00:00 +0900"
last_modified_at: "2024-12-23 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

## stack
![problem_ex](/assets/img/stack.png)

### 특징
- **LIFO(Last In, First Out):** 가장 나중에 들어온 데이터가 가장 먼저 나오는 자료구조 방식
- 뒤(위)에서만 추가/제거 가능

### 메서드
- **push():** 데이터를 스택에 추가
- **pop():** 스택에서 데이터를 제거(가장 마지막에 추가된 데이터)
- **top()/peek():** 스택의 가장 상단에 있는 데이터 확인

### 사용사례
- 재귀 호출처리
- 문자열 역순 변환: 문자열 역순으로 출력할 때
- 괄호검사: 여는 괄호와 닫는 괄호의 짝을 확인할 때
- DFS(깊이우선탐색): 그래프 탐색에서 경로 추적하기 위해 사용

```c++
stack<int> s;
s.push(1);
s.push(2);
s.push(3);
cout << s.top(); //출력: 3
s.pop(); //3 제거
cout << s.top(); //출력: 2
```


## queue
![problem_ex](/assets/img/queue.png)

### 특징
- **FIFO(First In, First Out):** 가장 먼저 들어온 데이터가 가장 먼저 나오는 자료구조 방식
- 앞에서 추가, 뒤에서 제거 가능

### 메서드
- **push()/enqueue():** 데이터를 큐에 추가
- **pop()/dequeue():** 큐에서 데이터를 제거(가장 먼저 들어온 데이터)
- **front():** 큐의 가장 앞에 있는 데이터 확인
- **back():** 큐의 가장 뒤에 있는 데이터 확인

### 사용사례
- BFS(너비우선탐색): 그래프 탐색에서 레벨 순서로 탐색하기 위해 사용

```c++
queue<int> q;
q.push(1);
q.push(2);
q.push(3);
cout << q.front(); //출력: 1
q.pop(); //1 제거
cout << q.front(); //출력: 2
```


## deque
![problem_ex](/assets/img/deque.png)
![problem_ex](/assets/img/deque_ex.png)

### 특징
- **Double Ended Queue:** 큐처럼 양쪽 끝에서 데이터를 추가하거나 제거할 수 있는 자료구조
- 앞쪽과 뒤쪽에서 모두 데이터를 추가하거나 제거 가능

### 메서드
- **push_front():** 덱의 앞에 데이터 추가
- **push_back():** 덱의 뒤에 데이터 추가
- **pop_front():** 덱의 앞에서 데이터 제거
- **pop_back():** 덱의 뒤에서 데이터 제거
- **front():** 덱의 앞에 있는 데이터 확인
- **back():** 덱의 뒤에 있는 데이터 확인

### 사용 사례
- 양방향 데이터 처리: 양쪽 끝에서 삽입/삭제가 필요할 때
- 문자열 문제: 회문(팰린드롬) 검사 등 양쪽에서 데이터를 처리하는 경우

```c++
deque<int> d;
d.push_back(1);
d.push_back(2);
d.push_front(0);
cout << d.front(); //출력: 0
cout << d.back(); //출력: 2
d.pop_front(); //0 제거
d.pop_back(); //2 제거
```