---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] 시간복잡도 비교"
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

## O(N)
- 입력크기 N에 비례하여 작업 횟수가 증가
- N이 두배가 되면 작업 시간도 두배가 됨

### 예시
- 책장을 N칸 가진 서재에서 특정 책을 찾는다고 했을 때, **O(N)은 첫번째 칸부터 마지막 칸까지 모든 칸을 차례로 확인하는 방식**
  - N칸을 모두 확인해야 하므로 칸이 많아질수록 시간이 비례해서 늘어남
    - N=10: 10번 작업
    - N=100: 100번 작업
    - N=1000: 1000번 작업

```c++
// 배열에서 특정 값을 찾는 O(N) 알고리즘
int linearSearch(vector<int> arr, int target) {
    for (int i = 0; i < arr.size(); i++) {
        if (arr[i] == target) {
            return i; // 값을 찾으면 반환
        }
    }
    return -1; // 값을 못 찾으면 -1 반환
}
```

## O(log N)
- 입력크기 N이 커질수록, 작업 횟수는 logN에 따라 천천히 증가
- N이 두배가 되더라도 작업 횟수는 한번 정도만 늘어남

### 예시
- 책장을 N칸 가진 서재에서 특정 책을 찾는다고 했을 때, **O(logN)은 중간부터 시작해서 절반씩 줄이는 방식**
  - N=1000일 때:
    1. 처음 500번째 칸에서 확인
    2. 찾는 책이 앞쪽에 있으면 1~499 사이로 범위를 줄임
    3. 다음엔 250번째 칸에서 확인
    - 이렇게 절반씩 줄여가며 탐색
    - 책장 칸이 많아져도 탐색 횟수는 상대적으로 적음

```c++
// 배열에서 특정 값을 찾는 O(log N) 알고리즘 (이진 탐색)
int binarySearch(vector<int> arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) {
            return mid; // 값을 찾으면 반환
        }
        if (arr[mid] < target) {
            left = mid + 1; // 오른쪽 반 탐색
        } else {
            right = mid - 1; // 왼쪽 반 탐색
        }
    }
    return -1; // 값을 못 찾으면 -1 반환
}
```
## O(N)과 O(log N)의 비교

|특징|O(N)|O(log N)|
|---|---|---|
|**작업 횟수 증가율**|입력 크기와 비례|입력 크기에 비례하지만 매우 느리게 증가|
|**효율성**|비효율적일 수 있음|큰 입력 데이터에서 매우 효율적|
|**비유**|하나하나 확인하는 방식|반씩 줄여가며 확인하는 방식|

## 정리
- O(N): 모든 데이터를 전부 확인해야 하는 경우 (예: 선형 탐색)
- O(log N): 절반씩 나누는 방식으로 빠르게 탐색하는 경우 (예: 이진 탐색)
  - 입력 크기가 커질수록 O(log N)이 O(N)보다 훨씬 효율적