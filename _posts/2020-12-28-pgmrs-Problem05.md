---
title: "다시 시작하는 코딩: Problem-05"
date: 2020-12-28 16:08:54 -0400
categories: [ 프로그래머스 ]
tags: [ 카카오 ]
---

[2018 카카오]n진수 게임: https://programmers.co.kr/learn/courses/30/lessons/17687

접근방법
--------
우선 범위(t*m)만큼의 n진수를 모두 나열하는 배열을 만들고, 해당 배열에서 필요한 인덱스 번호만을 가져오는
방법으로 푸는 것을 생각하였다.<br>
**expo 함수**를 통해 특정 숫자를 특정 진수로 출력하는 함수를 만들었다.
스택을 이용해서 n진수로 변환 시키니까 리스트에 반대로 들어가게 되고, 이를 정순서로 돌리기 위해
```python
a.reverse()
```
메소드를 사용하였다. 하지만 O(n)의 시간복잡도를 2번 돌리니까 O(n<sup>2</sup>)이 나왔고, 시간초과가 뜬다...<br>
그래서 n진수로 변환한 것을 list로 표현하지 않고 그냥 문자열 연산으로 해결했다.

전체 소스코드
------
```python
def solution(n, t, m, p):
    answer = ''
    array = ''
    # O(N)
    for i in range(t*m+1):
        array = array+expo(n,i)
    for i in range(t):
        answer += array[p+m*i-1]
    return answer

def expo(dimension, num):
    result = ''
    # O(log N)
    while num >= dimension:
        result = to_alphabet(num % dimension) + result
        num = int(num/dimension)
    result = to_alphabet(num) + result
    
    return result

def to_alphabet(num):
    if num == 10:
        return 'A'
    elif num == 11:
        return 'B'
    elif num == 12:
        return 'C'
    elif num == 13:
        return 'D'
    elif num == 14:
        return 'E'
    elif num == 15:
        return 'F'
    else:
        return str(num)
```
