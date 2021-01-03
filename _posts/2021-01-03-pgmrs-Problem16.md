---
title: "다시 시작하는 코딩: Problem-16"
date: 2021-01-03 16:38:19 -0400
categories: [ 프로그래머스 ]
tags: [ 정렬 ]
---

H-Index: https://programmers.co.kr/learn/courses/30/lessons/42747

접근방법
--------
1. 각 논문이 index회 이상 인용된 `num` 리스트를 생성한다.
2. 해당 리스트의 원소값과 인덱스 번호의 차를 구한다.
3. 번호의 차가 0에 가장 가까운 논문의 인덱스 번호가 곧 h-index이다.

> 다른 사람의 풀이를 살펴보니 더 쉬운 풀이가 많았다.

※다른 풀이법
-------------
```python
def solution(citations):
    citations = sorted(citations)
    answer = len(citations)
    for i in range(answer):
        if citations[i] >= answer-i:
            return answer-i
    return 0
```

1. 사전조건: 결국 답은 논문 발표 횟수 안에 존재한다.
2. 인용 횟수를 오름차순으로 정렬한다.
3. `눈문발표횟수 - 인덱스번호`를 하면 논문 인용횟수가 나온다
4. 그 중 최대값을 찾아 출력한다.

전체 소스코드
------
```python
def solution(citations):
    answer = 0
    citations.sort()
    num = []
    MAX = max(citations)

    for i in range(MAX + 1):
        count = 0
        for j in range(len(citations)):
            if citations[j] >= i:
                count += 1
        num.append(count)

    for i in range(len(num)):
        num[i] = abs(num[i] - i)
    MIN = 99999
    for i in range(len(num)):
        # 역전구간은 이전값을 가지고 와야한다
        if MIN > num[i]:
            MIN = num[i]
            answer = i

    return answer
```