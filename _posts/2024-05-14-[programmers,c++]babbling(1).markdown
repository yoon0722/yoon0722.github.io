---
classes: wide
toc: true
toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[programmers/C++] 옹알이(1)"
date: "2024-05-14 00:00:00 +0900"
last_modified_at: "2024-05-14 00:00:00 +0900"
categories:
  - programmers
tags:
  - c++
  - lv0
author_profile: true
sidebar:
    nav: docs
---

## 문제 설명
머쓱이는 태어난 지 6개월 된 조카를 돌보고 있습니다. 조카는 아직 "aya", "ye", "woo", "ma" 네 가지 발음을 최대 한 번씩 사용해 조합한(이어 붙인) 발음밖에 하지 못합니다. 문자열 배열 **babbling**이 매개변수로 주어질 때, 머쓱이의 조카가 발음할 수 있는 단어의 개수를 return하도록 solution 함수를 완성해주세요.

### 입출력 예

|babbling|result|
|---|---|
|["aya", "yee", "u", "maa", "wyeoo"]|1|
|["ayaye", "uuuma", "ye", "yemawoo", "ayaa"]|3|


## 코드 구현
<!-- <script src="https://gist.github.com/yoon0722/85fbe9421562363345d676d73a17a8b0.js"></script> -->
```c++
#include <string>
#include <vector>
#include <iostream>
using namespace std;

int solution(vector<string> babbling) {
    int answer = 0;
    vector<string> speak = {"aya", "ye", "woo", "ma"}; //가능한 발음
    
    for(string bab:babbling){ //babbling 배열에서 하나씩 불러오기
        vector<bool> babbool(bab.size(), false); //bab의 size만큼 false 생성
        
        for(int i=0; i<speak.size(); i++){ //speak 배열에서 하나씩 불러오기
            if(bab.find(speak[i]) != string::npos){ //babbling에 가능한 발음 있으면
                int startpos = bab.find(speak[i]); //가능한 발음 시작위치
                int speak_size = speak[i].size(); //speak 크기
                
                for(int j=startpos; j<startpos+speak_size; j++){
                    if(babbool[j]==false){
                        babbool[j]=true; //babbling에서 가능한 발음 true로 전환
                    }
                    else if(babbool[j]==true){
                        babbool[j]=false;
                    }
                }                
            }
        }
        bool all_true=true; //모든 요소가 true인지 확인하기 위한 변수 초기화
        
        for(bool b: babbool){ 
            if(b==0){ //c++에서 true=1, false=0으로 출력
                all_true=false;
                break;
            }
        }
        if(all_true){ //모든 요소가 true이면
            answer++;
        }
    }
    return answer;
}
```


## 공부한 내용
### 1. string.find() 함수
```c++
#include <string>
string str;
str.find(value);
```
'string' 클래스의 멤버 함수 중 하나로, 특정 문자열이 다른 문자열 안에 포함되어 있는지를 검사한다. 만약 포함되어 있다면, 그 위치(index)를 반환하고, 그렇지 않으면 'string::npos'를 반환한다.

**예시**
```c++
string str = "Hello World!"
size_t found = str.find("Wor");
if(found != string::npos){
    cout << "문자열에 'Wor'가 존재합니다." << endl;}
else{
    cout << "문자열에 'Wor'가 존재하지 않습니다." << endl;}
```

### 2. string::npos
문자열에서 특정 문자열을 찾지 못한 경우에 반환되는 특별한 상수이다.
string::find()함수는 문자열이 존재하지 않을 때 npos를 반환한다.


## Review
bool vector를 사용하여 해결했다.<br/>
예를 들어 **for(string bab:babbling)**에서 **bab**이 **"ayaye"**일때, **babbool={false, false, false, false, false}**가 된다.<br/>
**if(bab.find(speak[0]) != string::npos)**이라고 가정했을때, 
**"aya"**가 **"ayaye"**안에 포함되어 있으니까 **startpos=0**, **speak_size=3**이 된다.
**for(int j=0; j<3; j++)** 이므로 **babbool={false, false, false, false, false}**에서 **babbool={true, true, true, false, false}**가 된다.<br/>
이런식으로 babbool의 **모든 요소가 true**가 되면 answer+1이된다.<br/>
<br/>난이도 Lv.0임에도 불구하고 어려웠다.<br/> 
공부하자.

---
출처: 프로그래머스 코딩 테스트 연습, https://school.programmers.co.kr/learn/challenges