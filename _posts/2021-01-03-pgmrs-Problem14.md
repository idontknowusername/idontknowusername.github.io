---
title: "다시 시작하는 코딩: Problem-14"
date: 2021-01-03 13:22:04 -0400
categories: [ 프로그래머스 ]
tags: [ heap ]
---

이중우선순위큐: https://programmers.co.kr/learn/courses/30/lessons/42628

접근방법
--------
1. Insert 명령이 들어올때마다 2개의 힙(min heap, max heap)에 넣어준다.
2. Delete 명령이 들어올때마다 명령에 맞춰 min heap 혹은 max heap에서 pop 해준다.
3. pop 해준 value를 찾아 나머지 heap 에서 remove 한 다음, heapify를 통해 다시 heap 형태로 정렬해준다.

처음에 pop과 push 메소드 만을 이용해서 풀이하다 잘 안돼서
굉장히 무식한 방법으로 코드를 작성했다. 해당 코드가 정석적인 코드인지 잘 모르는 관계로 문제를 통과한 후, 다른사람들의 코드를 참고해봤다.<br>
결국 가장 교과서적인면서 알아보기 쉬운 방법은 min heap max heap 2개를 만드는 것이었다...

전체 소스코드
------
```python
import heapq

def solution(operations):
    answer = []
    MAX = []
    MIN = []
    
    for oper in operations:
        # Insert operation
        if oper[0] == 'I':
            num = int(oper.split(' ')[1])
            heapq.heappush(MIN, num)
            # max index: [1]
            heapq.heappush(MAX, (-num, num))
        # Delete operation
        else:
            op = int(oper.split(' ')[1])
            # delete max
            if op == 1 and len(MAX):
                dvalue = heapq.heappop(MAX)[1]
                MIN.remove(dvalue)
                heapq.heapify(MIN)
            # delete min
            elif op == -1 and len(MIN):
                dvalue = heapq.heappop(MIN)
                MAX.remove((-dvalue,dvalue))
                heapq.heapify(MAX)
    if len(MAX):
        answer.append(MAX[0][1])
        answer.append(MIN[0])
    else:
        answer.append(0)
        answer.append(0)
    return answer
```
