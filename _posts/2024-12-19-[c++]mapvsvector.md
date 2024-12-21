---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] map vs vector&lt;pair&gt;"
date: "2024-12-19 00:00:00 +0900"
last_modified_at: "2024-12-19 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

## map
```c++
#include <map>
```
- c++ 표준 템플릿 라이브러리(STL: Standard Template Library)에서 제공하는 표준 컨테이너
- 데이터를 키(key)와 값(value)의 쌍으로 저장
  - 키(key): 데이터를 식별하기 위한 고유한 값
  - 값(value): 키에 연결된 데이터

### 특징
- 이진탐색트리로 구현되어있어 삽입/탐색/삭제의 시간 복잡도는 O(log N)

#### 오름차순 정렬
- 키를 기준으로 오름차순 정렬된다.

```c++
map<int, string> mp;
mp[3] = "three";
mp[1] = "one";
mp[2] = "two";

for(auto& p: mp){
  cout << p.first << ":" << p.second << endl; 
}

//출력: 1:one, 2:two, 3:three
```

#### 내림차순 정렬법

```c++
map<int, string, greater<int>> mp;
```

#### 고유한 키
- 키는 고유하며 중복을 허용하지 않는다.

```c++
map<int, string> mp;
mp[1] = "one";
mp[1] = "1"; //기존의 키1의 값이 "1"로 변경
```

#### 키로 값 출력
- 기본적으로 키(key)로 값(value)을 찾는데 최적화 되어있다.

```c++
map<string, string> phoneBook;
phoneBook["Alice"] = "123-4567";
phoneBook["Bob"] = "987-6543";

cout << phoneBook["Alice"]; //출력: 123-4567
```
```c++
map<int, int> scores;
scores[101] = 90;
scores[102] = 80;

cout << scores[101]; //출력: 90 
```

## vector&lt;pair&gt;
```c++
#include <vector>
```
- c++ STL에서 제공하는 데이터 구조
- 두개의 데이터를 하나로 묶음

```c++
vector<pair<int, string>> vec;
```

- 데이터는 .first와 .second 멤버를 통해 접근 가능

```c++
vector<pair<int, string>> vec;

vec.push_back({1, "apple"});
vec.push_back({2, "banana"});
vec.push_back({3, "cherry"});

for(const auto& p: vec){
  cout << p.first << ":" << p.second << endl;
}
//출력: 1:apple 2:banana 3:cherry
```

- map처럼 키-값 구조는 아님

### 특징
#### 자동정렬 X
- 자동정렬되지 않고 입력한 순서대로 데이터를 저장하고 출력된다.

```c++
vector<pair<int, string>> vec;

vec.push_back({3, "three"});
vec.push_back({1, "one"});
vec.push_back({2, "two"});

for (auto& p : vec) {
  cout << p.first << ": " << p.second << endl;
}
//출력: 3:three, 1:one, 2:two
```
- 수동으로 sort를 사용해서 정렬할 수 있다.
  - pair의 첫번째 요소(.first)를 기준으로 정렬
  - 첫번째 요소가 같으면 두번째 요소(.second)를 기준으로 정렬

```c++
vector<pair<int, string>> vec = ({3, "cherry"}, {1, "apple"}, {2, "banana"});

sort(vec.begin(), vec.end());

for(const auto& p : vec){
  cout << p.first << p.second << endl;
}
// 출력: 1apple 2banana 3cherry
```
##### 예제) 좌표저장 및 정렬
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(){
  vector<pair<int, int>> points = ({3, 4}, {1, 2}, {5, 1}, {3, 2});

  sort(points.begin(), points.end());

  for(const auto& point : points){
    cout << point.first << ", " << point.second << endl;
  }
  // 1, 2
  // 3, 2
  // 3, 4
  // 5, 1
}
```

## map vs vector&lt;pair&gt;

|특징|map|vector&lt;pair&gt|
|---|---|---|
|키의 중복 허용|불가|허용|
|자동 정렬|자동정렬(키 기준)|정렬되지 않음(sort 사용)|
|검색 속도|빠름 (O(log N) 이진 트리 구조 사용)|느림(O(N) 루프 필요)|
|데이터 접근|키로 직접 접근 (myMap[key])|순차 접근 (vec[i].first, vec[i].second)|
|유연성|단일 키-값 쌍에 적합|여러 동일 키를 활용한 복잡한 데이터 표현 가능|

## 정리
- map
  - 키가 고유하며, 특정 키를 빠르게 검색하거나 값을 추가/갱신해야하는 경우 사용
- vector&lt;pair&gt;
  - 순서가 중요하거나, 정렬 기준이 자주 바뀌는 경우 사용
  - 키 값이 중복될 수 있는 경우