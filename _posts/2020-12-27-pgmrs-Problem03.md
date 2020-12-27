---
title: "다시 시작하는 코딩: Problem-03"
date: 2020-12-27 14:08:24 -0400
categories: [ 프로그래머스 ]
tags: [ 해시 ]
---

전화번호 목록: https://programmers.co.kr/learn/courses/30/lessons/42578

최초접근
--------
우선 dictionary로 각각의 옷들의 갯수를 정리했다.
그리고 나서 조합을 이용해 최소 한 벌의 옷을 입을 수 있는 경우의 수를 구하려 했지만
조합은 O(2<sup>n</sup>)의 시간복잡도를 가지기 때문에 입력 값의 길이가 조금만 길어져도
시간 초과가 났다.

해법
------
> 스파이는 하루에 최소 한 개의 의상을 입습니다.
여기서 착안해 스파이가 아무것도 입지 않는 경우까지 포함하여 value값을 **아무것도 입지않음** 상태를 추가해준다.
이번에는 value들의 곱으로 모든 조합의 갯수를 구한뒤, 아무것도 입지 않은 경우인 1을 빼주면 결과값이 나온다.
```python
def solution(clothes):
    answer = 1
    category = {}
    for i in range(len(clothes)):
        if clothes[i][1] in category:
            category[clothes[i][1]] += 1
        else:
            # 처음 key값을 넣을때는 안입는 경우도 생각해서 2를 넣어준다
            category[clothes[i][1]] = 2
    
    value = list(category.values())
    for i in range(len(value)):
        answer *= value[i]
    # 아무것도 입지 않은 경우를 빼준다
    answer -= 1
    return answer
```