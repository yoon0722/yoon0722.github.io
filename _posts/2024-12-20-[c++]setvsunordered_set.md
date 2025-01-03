﻿---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] set vs unordered_set"
date: "2024-12-20 00:00:00 +0900"
last_modified_at: "2024-12-20 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

## set
- 이진탐색트리(Red-Black Tree)로 구현
- 중복값 허용하지 않음
- 요소들이 **자동으로 정렬된 상태**로 저장되어 순서대로 데이터를 다루거나 순차적으로 탐색할 때 유리
    - {3, 1, 2}를 set에 넣으면 {1, 2, 3}으로 정렬
    - 상대적으로 시간이 더 걸릴 수 있다
- 삽입, 삭제, 검색의 시간복잡도는 O(log n)

```c++
#include <iostream>
#include <set>
using namespace std;

int main() {
    set<int> s;

    // 삽입
    s.insert(3);
    s.insert(1);
    s.insert(2);
    s.insert(3); // 중복값은 무시됨

    // 출력 (자동 정렬)
    for (auto x : s) {
        cout << x << " "; // 출력: 1 2 3
    }

    // 삭제
    s.erase(2); // 값 2 삭제
    for (auto x : s) {
        cout << x << " "; // 출력: 1 3
    }

    // 검색
    if (s.find(1) != s.end()) {
        cout << "1이 존재합니다." << endl;
    } else {
        cout << "1이 존재하지 않습니다." << endl;
    }

    return 0;
}
```

## unordered_set
- 해시 테이블 기반으로 구현
- 중복값 허용하지 않음
- 요소들이 **정렬되지 않은 상태**로 저장되기 때문에 순서가 중요한 경우에는 적합하지 않음
    - {3, 1, 2}를 unordered_set에 넣으면 저장 순서가 달라질 수 있음
- 삽입, 삭제, 검색의 평균 시간 복잡도는 O(1), 최악의 경우 O(n)

```c++
#include <iostream>
#include <unordered_set>
using namespace std;

int main() {
    unordered_set<int> us;

    // 삽입
    us.insert(3);
    us.insert(1);
    us.insert(2);
    us.insert(3); // 중복값은 무시됨

    // 출력 (정렬되지 않음)
    for (auto x : us) {
        cout << x << " "; // 출력 순서 예시: 3 1 2 (순서는 실행마다 다를 수 있음)
    }

    // 삭제
    us.erase(2); // 값 2 삭제
    for (auto x : us) {
        cout << x << " "; // 출력: 3 1 (순서는 실행마다 다를 수 있음)
    }
    cout << endl;

    // 검색
    if (us.find(1) != us.end()) {
        cout << "1이 존재합니다." << endl;
    } else {
        cout << "1이 존재하지 않습니다." << endl;
    }

    return 0;
}
```

## 정리
- set
    - 데이터를 **정렬된 상태**로 유지해야하는 경우
    - 순차적으로 데이터를 **정렬하여 출력**하거나 **범위 검색**이 필요한 경우 유용
- unordered_set
    - **빠른 삽입, 검색**이 중요한 경우
    - 순서와 상관없이 집합의 존재 여부를 빠르게 확인해야 하는 경우 유용

---

|특징|set|unordered_set|
|---|---|---|
|구현 방식|이진 탐색 트리 (Red-Black Tree 등)|해시 테이블 (Hash Table)|
|자동 정렬|정렬됨|정렬되지 않음|
|시간 복잡도|삽입, 삭제, 검색: O(log n)|삽입, 삭제, 검색: 평균 O(1), 최악 O(n)|
|성능|정렬이 필요할 때 유리|빠른 삽입과 검색이 필요할 때 유리|
|메모리 사용|트리 구조로 인한 추가 메모리 사용|해시 테이블로 인한 메모리 사용|
