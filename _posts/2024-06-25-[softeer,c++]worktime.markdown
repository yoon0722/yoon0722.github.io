---
layout: post
title:  "[Softeer/C++] 근무 시간"
date:   "2024-06-25 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["Softeer"]
tags: ["cpp", "lv1"] 
---

### 내 코드
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
---

### Review
풀이가 그닥 마음에 들지 않는다.

**출처:** Softeer, https://softeer.ai/practice/6254