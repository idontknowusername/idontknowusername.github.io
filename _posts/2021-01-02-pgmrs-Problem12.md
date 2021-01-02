---
title: "다시 시작하는 코딩: Problem-12"
date: 2021-01-02 17:30:15 -0400
categories: [ 프로그래머스 ]
tags: [ heap ]
---

더 맵게: https://programmers.co.kr/learn/courses/30/lessons/42626

접근방법
--------
처음엔 단순 정렬을 이용해서 스코빌 지수를 반복하여 섞었다.
```python
def solution(scoville, K):
    answer = 0
	
    while scoville[0] < K:
        scoville.sort()
        if len(scoville) == 1:
            return -1
        combi = comb(scoville.pop(0), scoville.pop(0))
        answer += 1
        scoville.append(combi)
        
    return answer

def comb(first, second):
    return first + 2*second
```
이 코드를 실행하면 테스트 케이스는 통과하지만 엄밀히 말해
`O(NlogN)`의 시간복잡도를 지닌 sort를 n번 수행하기 때문에
O(N<sup>2</sup>logN)의 시간 복잡도를 가졌기 때문에 효율성 테스트에서 모두 실패한다.
![효율성](/assets/img/problem12/1.png)

그래서 heap을 사용하기 위해 `heapq` 모듈을 import 한다.<br>
heap은 힙트리를 재구성하면서 logN의 시간복잡도를 가지기 때문에 전체 시간복잡도는 NlogN이다.<br>
단순히 min heap으로 구성한다음 똑같이 비교해주면 쉽게 구할 수 있다.

전체 소스코드
------
```python
import heapq

def solution(scoville, K):
    answer = 0
    heapq.heapify(scoville)
    while scoville[0] < K:
        if len(scoville) <= 1:
            return -1
        new = comb(heapq.heappop(scoville), heapq.heappop(scoville))
        heapq.heappush(scoville, new)
        answer += 1
        
    return answer

def comb(first, second):
    return first + 2*second
```
