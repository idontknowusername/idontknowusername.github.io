---
title: "다시 시작하는 코딩: Problem-10"
date: 2021-01-01 12:38:07 -0400
categories: [ 프로그래머스 ]
tags: [ 스택/큐 ]
---

프린터: https://programmers.co.kr/learn/courses/30/lessons/42587

접근방법
--------
*prioirities* 큐에 문제 요구사항대로 순서대로 연산을 해준다.<br>
**※중요한 것**은 각 연산이 진행될 때마다 목표의 인덱스 번호인 *location*이 어떻게 바뀌는지만 체크해주면 된다.

전체 소스코드
------
```python
def solution(priorities, location):
    answer = 0
    
    while True:
        important = max(priorities)
        cur = priorities.pop(0)
        # 더 중요한 작업이 있다면, 뒤로
        if important > cur:
            priorities.append(cur)
            # 내가 요청한 작업이 맨 앞이 아니라면
            if location:
                location -= 1
            # 맨 앞이라면
            else:
                location = len(priorities) - 1
        # 없다면, 인쇄
        else:
            answer += 1
            # 내가 요청한 작업이 인쇄됐다면 루프 종료
            if location:
                location -= 1 # 인쇄되면 배열 길이가 1 짧아져서 위치도 빼준다.
                continue
            else:
                break
    
    return answer
```
