---
layout: post
title:  "[C++] transform 함수"
date:   "2024-06-07 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["C++"]
tags: ["cpp"]
---

### transform(v.begin(), v.end(), new_v.begin(), ::tolower/::toupper)
- `<algorithm>`헤더에 정의되어 있다.
- v.begin()부터 v.end()까지의 범위에 있는 요소들에 주어진 함수를 적용시킨다.
- 세 번째 인자인 new_v.begin()에 변환된 값들을 저장한다. 이렇게 하면 원래 v벡터를 변경하지 않고도 변환된 결과를 new_v벡터에 저장할 수 있다.
- 세 번째 인자에 v.begin()값을 그대로 사용해 줌으로써 변환된 값들을 기존의 v벡터에 덮어쓸 수 있다.

---

### 예시 1
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
// 숫자의 제곱을 계산하는 함수
int square(int x) {
    return x * x;
}

int main() {
    vector<int> v = {1, 2, 3, 4, 5};
    vector<int> result(v.size()); 

    transform(v.begin(), v.end(), result.begin(), square); 
    //square 적용한 값을 result 벡터에 저장
    for (int num : result) {
        cout << num << " ";
    }

    return 0;
}
```

### 예시 2
```c++
    string word;
    cin >> word;
    
    transform(word.begin(), word.end(), word.begin(), ::toupper);
    //문자열값을 모두 대문자로 변경해준다.
```
