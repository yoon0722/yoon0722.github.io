---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[Softeer/C++] 성적 평균"
date: "2024-06-27 00:00:00 +0900"
last_modified_at: "2024-06-27 00:00:00 +0900"
categories:
  - Softeer
tags:
  - c++
  - lv3
author_profile: true
sidebar:
    nav: docs
---

## 문제 설명
![problem_ex](/assets/img/6294_1.png)

### 입출력 예시
![problem_ex](/assets/img/6294_2.png)

## 코드 구현
```c++
#include<iostream>
#include<vector>
#include<iomanip>
using namespace std;

int main(int argc, char** argv)
{
    int N, K; //학생 수 N, 구간 수 K
    cin >> N >> K;
    //vector<int> scores(N);
    int scores[N];
    for(int i=1; i<=N; i++){
        int score;
        cin >> score;
        //scores.push_back(score);
        scores[i]=score;
    }
    for(int i=0; i<K; i++){
        int A, B;
        double totalScores=0;
        cin >> A >> B;
        for(int j=A; j<=B; j++){
            totalScores+=scores[j];
        }
        int Students=B-A+1;
        double average=totalScores/Students;
        cout << fixed << setprecision(2) << average << endl;
    }
   return 0;
}
```
전에 공부한 [[C++] 소수점 구하기 setprecision(), fixed]({% post_url 2024-05-16-[c++]setprecision(),fixed %})이 떠올라서 사용해봤다.
<br/>'setprecision'은 지정한 자릿수로 숫자를 표시할 때 필요한 경우 반올림도 수행한다.

---
**출처:** Softeer, https://softeer.ai/practice/6294