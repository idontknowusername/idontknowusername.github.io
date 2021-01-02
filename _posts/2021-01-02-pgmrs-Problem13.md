---
title: "다시 시작하는 코딩: Problem-13"
date: 2021-01-02 19:30:25 -0400
categories: [ 프로그래머스 ]
tags: [ heap ]
---

디스크 컨트롤러: https://programmers.co.kr/learn/courses/30/lessons/42627

접근방법
--------
heap에 대한 개념이 약해서 비교적 어렵게 해결한 문제다...<br>
현재 시간 기준으로 대기 가능한 작업을 다 넣어주고 minheap을 통해 짧은 수행시간의 작업을 하나씩 수행시킨다.
모든 작업이 대기열에 들어가면 대기열에 있는 작업을 짧은 순서대로 전부 수행시킨다.

전체 소스코드
------
```python
import heapq

def solution(jobs):
    answer = 0
    time = 0
    count = len(jobs)
    hq = []
    jobs.sort()

    # 모든 작업이 빠질때까지
    while len(jobs):
        # 현재 대기 시킬수 있는 모든 작업을 빼준다,
        while len(jobs) and jobs[0][0] <= time:
            # hq[0:수행시간, 1:들어온시간]
            heapq.heappush(hq,[jobs[0][1],jobs[0][0]])
            jobs.pop(0)
        # 만약 수행가능한 작업이 있다면 수행한다.
        if len(hq):
            out = heapq.heappop(hq)
            answer += out[0] + (time - out[1])
            time += out[0]
        else:
            time += 1
    # 남아있는 힙은 그냥 순서대로 다 빼준다
    while len(hq):
        out = heapq.heappop(hq)
        answer += out[0] + (time - out[1])
        time += out[0]
    
    return int(answer/count)
```
