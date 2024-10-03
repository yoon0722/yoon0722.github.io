---
#classes: wide
#toc: true
#toc_label: "My Table of Contents"
#toc_icon: "cog"
#layout: post
title: "[프로그래머스/C++] 동영상 재생기"
#date: "2024-10-03 00:00:00 +0900"
last_modified_at: "2024-10-03 00:00:00 +0900"
categories: 
    - Jekyll #["프로그래머스"]
#tags: ["cpp", "lv0"]
posts: 2017
---

### 문제 설명
당신은 동영상 재생기를 만들고 있습니다. 당신의 동영상 재생기는 10초 전으로 이동, 10초 후로 이동, 오프닝 건너뛰기 3가지 기능을 지원합니다. 각 기능이 수행하는 작업은 다음과 같습니다.

- 10초 전으로 이동: 사용자가 "prev" 명령을 입력할 경우 동영상의 재생 위치를 현재 위치에서 10초 전으로 이동합니다. 현재 위치가 10초 미만인 경우 영상의 처음 위치로 이동합니다. 영상의 처음 위치는 0분 0초입니다.
- 10초 후로 이동: 사용자가 "next" 명령을 입력할 경우 동영상의 재생 위치를 현재 위치에서 10초 후로 이동합니다. 동영상의 남은 시간이 10초 미만일 경우 영상의 마지막 위치로 이동합니다. 영상의 마지막 위치는 동영상의 길이와 같습니다.
- 오프닝 건너뛰기: 현재 재생 위치가 오프닝 구간(op_start ≤ 현재 재생 위치 ≤ op_end)인 경우 자동으로 오프닝이 끝나는 위치로 이동합니다.

<br/>동영상의 길이를 나타내는 문자열 video_len, 기능이 수행되기 직전의 재생위치를 나타내는 문자열 pos, 오프닝 시작 시각을 나타내는 문자열 op_start, 오프닝이 끝나는 시각을 나타내는 문자열 op_end, 사용자의 입력을 나타내는 1차원 문자열 배열 commands가 매개변수로 주어집니다. 이때 사용자의 입력이 모두 끝난 후 동영상의 위치를 "mm:ss" 형식으로 return 하도록 solution 함수를 완성해 주세요.

### 입출력 예

|video_len|pos|op_start	|op_end| commands|	result
|---|---|
"34:33"|"13:00"|"00:55"|"02:55"|["next", "prev"]|"13:00"
"10:55"|"00:05"|"00:15"|"06:55"|["prev", "next", "next"]|"06:55"
"07:22"|"04:05"|"00:15"|"04:07"|["next"]|"04:17"

### 내 코드

```c++
#include <string>
#include <vector>
#include <iostream>
using namespace std;

string solution(string video_len, string pos, string op_start, string op_end, vector<string> commands) {
    string answer = "";
    
    int sec_op_start=0;
    int sec_op_end=0;
    int sec_video_len=0;
    
    sec_op_start+=(op_start[0]-'0')*600;
    sec_op_start+=(op_start[1]-'0')*60;
    sec_op_start+=(op_start[3]-'0')*10;
    sec_op_start+=(op_start[4]-'0');
    
    sec_op_end+=(op_end[0]-'0')*600;
    sec_op_end+=(op_end[1]-'0')*60;
    sec_op_end+=(op_end[3]-'0')*10;
    sec_op_end+=(op_end[4]-'0');
    
    sec_video_len+=(video_len[0]-'0')*600;
    sec_video_len+=(video_len[1]-'0')*60;
    sec_video_len+=(video_len[3]-'0')*10;
    sec_video_len+=(video_len[4]-'0');
    
    for(int i=0; i<commands.size(); i++){

        int sec_pos=0;
        sec_pos+=(pos[0]-'0')*600;
        sec_pos+=(pos[1]-'0')*60;
        sec_pos+=(pos[3]-'0')*10;
        sec_pos+=(pos[4]-'0');
        
        if(op_start<=pos && pos<=op_end){ //오프닝 건너뛰기
            pos=op_end;
        }
        
        int num=0;

        if(commands[i]=="next"){
            
            if(pos[3]=='5'){ //십초대 자리가 5이면(6부터 1시간)
                pos[3]='0'; //십초대 자리를 0으로 초기화
                if(pos[1]=='9'){ //일분대에 9가 있으면
                    pos[1]='0'; //일분대를 0으로 초기화
                    num=(pos[0]-'0')+1; //십초대+1
                    pos[0]='0'+num;
                }
                else{
                    num=(pos[1]-'0')+1;
                    pos[1]='0'+num;
                } //일분대가 9가 아니면 1분 추가
            }
            
            else{
                num=(pos[3]-'0')+1;
                pos[3]='0'+num;
            } //50초대가 아니면 10분 추가
            
            sec_pos=0;
            sec_pos+=(pos[0]-'0')*600;
            sec_pos+=(pos[1]-'0')*60;
            sec_pos+=(pos[3]-'0')*10;
            sec_pos+=(pos[4]-'0');

            if(sec_video_len<sec_pos){
                pos=video_len;
            }

        }
        
        else if(commands[i]=="prev"){
            
            if(pos[3]=='0'){ //십초대 자리가 0이면
                if(pos[1]!='0'){
                    num=(pos[1]-'0')-1; //일분대에서 -1분
                    pos[1]='0'+num;
                    pos[3]='5'; //-1분 -> +60초 -10초
                }
                else if(pos[1]=='0'){
                    if(pos[0]!='0'){
                        num=(pos[0]-'0')-1; //십분대 자리-1
                        pos[0]='0'+num;
                        pos[1]='9'; //-10분 -> +10분 - 1분
                        pos[3]='5'; //-1분 -> +60초 -10초
                    }
                    else if(pos[0]=='0'){
                        pos = "00:00";
                    }
                }
            }
            
            else{
                num=(pos[3]-'0')-1;
                pos[3]='0'+num;
            } //십초대 자리가 0이 아니면 10초 빼기
            
        }
        
        sec_pos=0;
        sec_pos+=(pos[0]-'0')*600;
        sec_pos+=(pos[1]-'0')*60;
        sec_pos+=(pos[3]-'0')*10;
        sec_pos+=(pos[4]-'0');
        
        if(op_start<=pos && pos<=op_end){ //오프닝 건너뛰기
            pos=op_end;
        }
        
    }
    
    answer = pos;
    return answer;
}

```

### Review
일단 푸는것을 목표로 무작정 풀어봤다.
반복되는 코드가 많아 매우 비효율적이라 생각해 이번엔 좀 더 효율적인 코드작성을 위해 다시 풀어봤다. 

---

```c++
#include <string>
#include <vector>
#include <iostream>
using namespace std;

int timetoSec(string time){
    int sec=0;
    sec+=(time[0]-'0')*600; //'0'=48
    sec+=(time[1]-'0')*60;
    sec+=(time[3]-'0')*10;
    sec+=(time[4]-'0');
    return sec;
}

string sectoTime(int sec){
    string time="";
    int minutes=sec/60;
    int seconds=sec%60;
    time+=(minutes/10)+'0'; //3+48=51='3'
    time+=(minutes%10)+'0';
    time+=':';
    time+=(seconds/10)+'0';
    time+=(seconds%10)+'0';
    return time;
}

string solution(string video_len, string pos, string op_start, string op_end, vector<string> commands) {
    string answer = "";

    int sec_op_start=timetoSec(op_start);
    int sec_op_end=timetoSec(op_end);
    int sec_video_len=timetoSec(video_len);
    int sec_pos=timetoSec(pos);
    
    for(int i=0; i<commands.size(); i++){
        
        if(sec_op_start<=sec_pos && sec_pos<=sec_op_end){ //오프닝 건너뛰기
            sec_pos=sec_op_end;
        }
        
        if(commands[i]=="next"){
            sec_pos+=10;
            
            if(sec_pos>sec_video_len){ //영상의 마지막 위치로 이동
                sec_pos=sec_video_len;
            }
        }
        
        else if(commands[i]=="prev"){
            sec_pos-=10;      
            
            if(sec_pos<0){
                sec_pos=0;
            }
        }
        
        if(sec_op_start<=sec_pos && sec_pos<=sec_op_end){ //오프닝 건너뛰기
            sec_pos=sec_op_end;
        }
        
    }
    
    answer = sectoTime(sec_pos);
    
    return answer;
}
```
---
출처: 프로그래머스 코딩 테스트 연습, https://school.programmers.co.kr/learn/challenges