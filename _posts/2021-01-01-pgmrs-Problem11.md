---
title: "다시 시작하는 코딩: Problem-11"
date: 2021-01-01 12:51:11 -0400
categories: [ 프로그래머스 ]
tags: [ 정렬 ]
---

K번째수: https://programmers.co.kr/learn/courses/30/lessons/42748

접근방법
--------
쉬어가는 L1 문제

전체 소스코드
------
```python
def solution(array, commands):
    answer = []
    
    for command in commands:
        cur = array[command[0]-1:command[1]]
        cur.sort()
        answer.append(cur[command[2] - 1])
        
    return answer
```
