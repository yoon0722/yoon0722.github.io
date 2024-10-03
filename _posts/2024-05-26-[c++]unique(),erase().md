---
layout: post
title:  "[C++] 중복원소 제거 (sort, unique, erase)"
date:   "2024-05-26 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["C++"]
tags: ["cpp", "백준"]
---

### sort()
- 오름차순으로 정렬해준다.
```c++
sort(vector.begin(), vector.end()); //vector={1,2,3,3,4,4,4,5}
```
unique() 함수를 사용하기 전에 sort()가 먼저 되어있어야 한다.

### unique()
- 중복되는 원소들은 맨 뒤로 배치된다.
```c++
unique(vector.begin(), vector.end()); //vector={1,2,3,4,5,3,4,4}
```

### erase()
- 중복되는 원소들을 제거해준다.
```c++
vector.erase(unique(vector.begin(), vector.end()), vector.end()); //vector={1,2,3,4,5}
```
---

### [백준 3052번] 나머지
```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main(){
    int num;
    vector<int> n;
    for(int i=0; i<10; i++){
        cin >> num;
        n.push_back(num%42);
    }
    sort(n.begin(), n.end());
    n.erase(unique(n.begin(), n.end()), n.end());
    
    cout << n.size();

    return 0;
}
```

