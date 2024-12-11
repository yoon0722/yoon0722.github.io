---
#classes: wide
#toc: true
#toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[Softeer/C++] 근무 시간"
date: "2024-06-25 00:00:00 +0900"
last_modified_at: "2024-06-25 00:00:00 +0900"
categories:
  - Softeer
tags:
  - c++
  - lv1
author_profile: true
sidebar:
    nav: docs
---

### 첫 풀이
```c++
#include<iostream>
#include<string>
#include<sstream>
using namespace std;

int main(int argc, char** argv){
    int Total=0;
    
    for(int i=0; i<5; i++){
        string time, startTime, endTime;
        getline(cin, time);
        stringstream ss(time);
        getline(ss, startTime, ' ');
        getline(ss, endTime);
    
        string startHour, startMinute, endHour, endMinute;
        stringstream ssStart(startTime);
        getline(ssStart, startHour, ':');
        getline(ssStart, startMinute);
        int SH, StartTotalM; 
        SH=stoi(startHour);
        StartTotalM=(SH*60)+stoi(startMinute);
        
        stringstream ssEnd(endTime);
        getline(ssEnd, endHour, ':');
        getline(ssEnd, endMinute);
        int EH, EndTotalM;
        EH=stoi(endHour);
        EndTotalM=(EH*60)+stoi(endMinute);
    
        Total+=EndTotalM-StartTotalM;
    
    }
    cout << Total;
    return 0;
}
```
답은 맞지만 중복되고 불필요한 코드가 많은 것 같다.
<br/>좀 더 간단하게 풀 수 있는 방법이 있을 것 같아 다시 풀어봤다.

### 두번째 풀이
```c++
#include<iostream>
#include<string>

using namespace std;

int main(int argc, char** argv){
    int Total=0;

    for(int i=0; i<5; i++){
        string time;
        getline(cin, time);
        string startHour = time.substr(0,2);
        string startMinute = time.substr(3,2);
        string endHour = time.substr(6,2);
        string endMinute = time.substr(9,2);
        int TotalStartMin = stoi(startHour)*60 + stoi(startMinute);
        int TotalEndMin = stoi(endHour)*60 + stoi(endMinute);
        Total += TotalEndMin - TotalStartMin;
    }
    cout << Total;
    return 0;
}
```
처음 풀었을 때 보다 단순하게 접근해서 풀어봤다.

---


**출처:** Softeer, https://softeer.ai/practice/6254