---
layout: post
title:  "[C++] 소수점 구하기 setprecision(), fixed"
date:   "2024-05-16 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["C++"]
tags: ["cpp"]
---

### setprecision()
setprecision(n) : 정수+소수자리를 합해서 n만큼 출력된다.

```c++
#include <iostream>
#include <iomanip> //setprecision(), fixed

using namespace std;

int main(){
    double number = 3.141592
    cout << setprecision(2) << number << endl;
    
    return 0;
}

// 출력값 : 3.1
```

### fixed

```c++
#include <iostream>
#include <iomanip>

using namespace std;

int main(){
    double number = 3.141592
    cout << fixed << setprecision(2) << number << endl;
    
    return 0;
}

// 출력값 : 3.14
```