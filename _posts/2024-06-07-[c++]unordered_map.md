---
layout: post
title:  "[C++] unordered_map<>"
date:   "2024-06-07 00:00:00 +0900"
#last_modified_at: "2024-05-03 00:00:00 +0900"
categories: ["C++"]
tags: ["cpp"]
---

### unordered_map<int, int> map;
- `<unordered_map>`헤더에 정의되어 있다.
- 해시 테이블을 기반으로 하는 연관 컨테이너이다.
- 평균 시간 복잡도는 O(1)이다.

---

### map VS unordered_map

#### map
- 이진 검색 트리로 구현된다.
- 키가 항상 정렬된 순서로 저장된다.
- 삽입, 삭제, 검색 연산의 시간 복잡도는 O(log n)이다.
- 요소가 정렬된 순서로 유지되어야 할 떄 적합하다.

#### 예시
```c++
#include <iostream>
#include <map>
int main(){
    map<int, int> orderedMap;
    orderedMap[3] = "Three";
    orderedMap[1] = "One";
    orderedMap[2] = "Two";

    // 정렬된 순서 O
    for (const auto& pair : orderedMap) {
        std::cout << "Key: " << pair.first << ", Value: " << pair.second << std::endl;
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

#### 예시
```c++
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> unorderedMap;
    unorderedMap[3] = "Three";
    unorderedMap[1] = "One";
    unorderedMap[2] = "Two";

    // 정렬된 순서 X
    for (const auto& pair : unorderedMap) {
        std::cout << "Key: " << pair.first << ", Value: " << pair.second << std::endl;
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

### [백준 1157번] 단어 공부
```c++

```

