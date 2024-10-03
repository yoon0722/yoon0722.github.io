---
layout: post
title:  "[C++] binary_search()"
date:   "2024-05-26 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["C++"]
tags: ["cpp", "백준"]
---

### binary_search(vector_begin, vector_end, find_value)
- `<algorithm>` 헤더에 정의되어 있다.
- 데이터가 정렬 sort() 되어 있다는 가정하게 사용가능하다.
- vector_begin은 시작주소, vector_end는 끝주소, find_value는 찾고자 하는 값이다.
- bool type으로 find_value가 있으면 true(1), 없으면 false(0)을 반환한다.

---

### [백준 5597번] 과제 안 내신 분..?
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int n;
    vector<int> student(30); //1-30번까지의 학생
    vector<int> missing_student(28); //제출한 28명의 학생
    
    for(int i=0; i<30; i++){
        student[i] = i+1;
    }

    for(int i=0; i<28; i++){
        cin >> n;
        missing_student[i]=n;
    }

    sort(missing_student.begin(), missing_student.end());

    for(int i=0; i<30; i++){
        if (!binary_search(missing_student.begin(), missing_student.end(), student[i])) {
            cout << student[i] << "\n";
        }
    }

    return 0;
}
```

