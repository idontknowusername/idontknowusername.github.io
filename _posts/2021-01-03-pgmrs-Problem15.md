---
title: "다시 시작하는 코딩: Problem-15"
date: 2021-01-03 15:21:39 -0400
categories: [ 프로그래머스 ]
tags: [ 정렬 ]
---

가장 큰 수: https://programmers.co.kr/learn/courses/30/lessons/42746

접근방법
--------
처음에는 각 원소의 자리수를 비교한다고 생각하여 코드가 상당히 복잡하고 0이 있는경우 예외가 너무 많아 풀리지 않았다.<br>
다른 사람들의 힌트를 얻어 문자열로 사전순 정렬을 하는 방법으로 간단하게 풀 수 있었다.

1. 각 원소는 1000의 자리 이하이기 때문에 각 자리수의 비교를 위해서 문자열로 치환하여 3번씩 붙여준다.
2. 해당 문자열 배열을 사전 역순으로 정렬한다.
3. 정렬된 배열의 큰 순서대로 원 문자열을 출력해준다.


전체 소스코드
------
```python
def solution(numbers):
    answer = ''
    token = []
    
    if not sum(numbers):
        return '0'
    
    # 각 자리를 3번씩 붙여서 문자열로 저장
    for num in numbers:
        token.append(str(num)*3)
    
    # 사전 역순으로 정렬
    token.sort(reverse=True)
    for i in token:
        for j in range(len(i) // 3):
            answer += i[j]
    print(token)
    # 각 자리수 별로 찢어서 token에 저장
    '''
    for i in range(len(numbers)) :
        token.append([])
        while numbers[i]:
            token[i].append(numbers[i] % 10)
            numbers[i] //= 10

    for i in range(len(token)):
        temp = token.pop()
        temp.reverse()
        for i in range(len(temp)):
            answer += str(temp[i])
    '''
    return answer
```
