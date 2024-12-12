---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] vector에서의 push_back() 함수"
date: "2024-05-25 00:00:00 +0900"
last_modified_at: "2024-05-25 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
  - baekjoon
author_profile: true
sidebar:
    nav: docs
---

## push_back()
- vector의 끝에 새로운 요소를 추가하는데 사용한다.

## vector 초기화 문제

**잘못된 코드**
```c++
int N;
cin >> N;

vector<int>A;

for(int i=0; i=N; i++){
	cin >> A[i];
}
```

에러가 뜬다.
<br/>초반에 vector를 선언해줄 때 vector의 크기를 미리 지정해주지 않으면 'push_back'함수를 사용해서 요소를 추가해 주어야 한다.


**정정 코드**
```c++
int N;
cin >> N;

vector<int>A;

for(int i=0; i=N; i++){
	int num;
	cin >> num;
	A.push_back(num);
}
```
이런식으로 수정해 주어야한다.


## [백준 10818번] 최소, 최대
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);

    int N;
    cin >> N;
    vector<int> A(N);
    
    for(int i=0; i<N; i++){
        int num;
        cin >> num;
        A.push_back(num);
    }

    int min = *min_element(A.begin(), A.end());
    int max = *max_element(A.begin(), A.end());

    cout << min << " " << max << endl;

    return 0;
}
```
이상하게 계속 min값이 0이 나왔다.
<br/>알고보니 vector값을 처음에 N으로 초기화 시켜줘서 앞의 N값들이 0으로 채워진 후에 'push_back'의 정의 'vector의 끝에 새로운 요소를 추가하는데 사용' 대로 그 뒤에 새로운 값들이 추가된 것 이었다.
<br/>push_back의 이해도가 부족했던것 같다.