---
title: "다시 시작하는 코딩: Problem-17"
date: 2021-01-03 16:57:25 -0400
categories: [ 프로그래머스 ]
tags: [ 완전탐색 ]
---

모의고사: https://programmers.co.kr/learn/courses/30/lessons/42840

접근방법
--------
1. 1번 2번 3번 수포자별 정답을 찍는 리스트를 만든다.
2. 입력값 `answers`를 처음부터 탐색하면서 모듈러 연산을 통해 수포자의 정답과 일치하면 점수를 1 올려준다.
3. 최대값과 일치하는 모든 인덱스를 출력한다.

전체 소스코드
------
```python
def solution(answers):
    answer = []
    p1 = [1,2,3,4,5]
    p2 = [2,1,2,3,2,4,2,5]
    p3 = [3,3,1,1,2,2,4,4,5,5]
    score = [0,0,0,0]
    for i in range(len(answers)):
        if answers[i] == p1[i%5]:
            score[1] += 1
        if answers[i] == p2[i%8]:
            score[2] += 1
        if answers[i] == p3[i%10]:
            score[3] += 1

    max_score = max(score)
    for i in range(1,len(score)):
        if score[i] == max_score:
            answer.append(i)
            
    return answer
```