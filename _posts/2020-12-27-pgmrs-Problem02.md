---
title: "다시 시작하는 코딩: Problem-02"
date: 2020-12-27 13:31:59 -0400
categories: [ 프로그래머스 ]
tags: [ 해시 ]
---

전화번호 목록: https://programmers.co.kr/learn/courses/30/lessons/42577

최초접근
--------
모든 인덱스를 순차적으로 비교하면 O(n<sup>2</sup>)의 시간복잡도를 가질거 같아
우선 정렬을 했다. 정렬을 하고 나면 같은 substr으로 시작하는 문자열은
길이가 짧은 것이 앞으로 온다는 것을 이용해 n번 문자열과 n+1번 문자열의 substr을 단순
비교 하는 방식으로 코드를 작성하였다.
```python
def solution(phone_book):
    answer = True
    phone_book.sort()
    for i in range(len(phone_book)-1):
        if phone_book[i+1][:len(phone_book[i])] == phone_book[i]:
            answer = False
            break
    return answer
```

해법
------
안될거라고 생각하고 고칠생각으로 채점을 진행했는데 한번에 통과해서 당황스럽네...