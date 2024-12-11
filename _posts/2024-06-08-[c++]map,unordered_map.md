---
#classes: wide
#toc: true
#toc_label: "My Table of Contents"
#toc_icon: "cog"
layout: single
title: "[C++] map vs unordered_map"
date: "2024-06-08 00:00:00 +0900"
last_modified_at: "2024-06-08 00:00:00 +0900"
categories:
  - C++
tags:
  - c++
author_profile: true
sidebar:
    nav: docs
---

### unordered_map
- `<unordered_map>`헤더에 정의되어 있다.
- unordered_map<int, string> myMap와 같은 형식으로 사용한다.
- 해시 테이블을 기반으로 하는 연관 컨테이너이다.
- 평균 시간 복잡도는 O(1)이다.

---

### map vs unordered_map 

#### map
- 이진 검색 트리로 구현된다.
- 키가 항상 정렬된 순서로 저장된다.
- 삽입, 삭제, 검색 연산의 시간 복잡도는 O(log n)이다.
- 요소가 정렬된 순서로 유지되어야 할 떄 적합하다.

#### 예시
```c++
#include <iostream>
#include <map>
using namespace std;

int main(){
    map<int, string> orderedMap;
    orderedMap[3] = "Three";
    orderedMap[1] = "One";
    orderedMap[2] = "Two";

    // 정렬된 순서 O
    for (const auto& pair : orderedMap) {
        cout << "Key: " << pair.first << ", Value: " << pair.second << endl;
    }

    return 0;
}

// 출력값
Key: 1, Value: One
Key: 2, Value: Two
Key: 3, Value: Three

```

---

#### unordered_map
- 해시 테이블로 구현된다.
- 키의 순서가 보장되지 않는다.
- 평균적으로 삽입, 삭제, 검색 연산의 시간 복잡도는 O(1)이다.
- 순서가 중요하지 않고, 빠른 검색과 삽입이 중요한 경우 적합하다.

#### 예시 1
```c++
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<int, string> unorderedMap;
    unorderedMap[3] = "Three";
    unorderedMap[1] = "One";
    unorderedMap[2] = "Two";

    // 정렬된 순서 X
    for (const auto& pair : unorderedMap) {
        cout << "Key: " << pair.first << ", Value: " << pair.second << endl;
    }

    return 0;
}

/// 출력값 
Key: 3, Value: Three
Key: 2, Value: Two
Key: 1, Value: One

/// 또는
Key: 1, Value: One
Key: 3, Value: Three
Key: 2, Value: Two

/// 또는
Key: 2, Value: Two
Key: 1, Value: One
Key: 3, Value: Three

//...

```
내부적으로 해시 테이블을 사용하므로, 요소의 순서는 저장된 순서와 다를 수 있으며 예측할 수 없다.
<br/> 순서가 보장되지 않기 때문에 실행할 때마다 결과가 다를 수 있다.

#### 예시 2 - 삽입, 삭제
```c++
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<int, string> myMap;

    // 요소 추가 방법 1: operator[]
    myMap[1] = "One";
    myMap[2] = "Two";

    // 요소 추가 방법 2: insert
    myMap.insert({3, "Three"});
    myMap.insert(make_pair(4, "Four"));

    // { {1, "One"}, {2, "Two"}, {4, "Four"}, {3, "Three"} } 
    // 이렇게 insert 됐다고 가정

    // 키를 이용하여 요소 삭제
    myMap.erase(2);

    // { {1, "One"}, {4, "Four"}, {3, "Three"} } 
    // key2 삭제

    return 0;
}

```