---
title: "다시 시작하는 코딩: Problem-06"
date: 2020-12-28 16:54:41 -0400
categories: [ 프로그래머스 ]
tags: [ 해시 ]
---

[2018 카카오]비밀지도: https://programmers.co.kr/learn/courses/30/lessons/17681

접근방법
--------
arr1과 arr2를 동시에 2진수로 변환하면서 둘중 하나라도 1이면 벽으로, 아니면 빈공간으로 두면 쉽게 풀린다.

전체 소스코드
------
```python
def solution(n, arr1, arr2):
    answer = []
    for i in range(n):
        answer.append(expo(n,arr1[i],arr2[i]))
    return answer

def expo(dimension, num1, num2):
    result = ''
    while num1 >= 1 or num2 >= 1:
        # 둘중 하나라도 벽이라면
        if num1 % 2 or num2 % 2:
            result = '#' + result
        else:
            result = ' ' + result
        num1 = int(num1/2)
        num2 = int(num2/2)
    # 필요한 차원보다 적은 숫자가 들어왔을때 여백 채워주기
    cond = dimension-len(result)
    for i in range(cond):
        result = ' ' + result
    return result
```
