---
title: "Problem-25: 소수 찾기"
date: 2021-01-12 19:26:59 -0400
categories: [ 프로그래머스 ]
tags: [ 완전탐색 ]
---

소수 찾기: https://programmers.co.kr/learn/courses/30/lessons/42839

문제 설명
--------
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

제한사항
--------
+ numbers는 길이 1 이상 7 이하인 문자열입니다.
+ numbers는 0~9까지 숫자만으로 이루어져 있습니다.
+ 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

 
입출력 예
-------

|numbers|return|
|------|---|
|"17"|3|
|"011"|2|

```
예제 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.
+ 11과 011은 같은 숫자로 취급합니다.
```

접근방법
--------
1. 소수인지 판별하는 함수 `prime` 생성
2. `permutations`를 이용해 모든 순열을 만들어 소수인지 판별하고 기존 리스트에 없다면 append
3. primes 리스트 길이 출력

전체 소스코드
------
```python
from itertools import permutations

def solution(numbers):
    answer = 0
    primes = []
    length = len(numbers) + 1

    for i in range(1,length):
        temp = list(map(''.join, permutations(numbers, i)))
        # print(temp)
        for j in temp:
            n = int(j)
            # 기존 배열에 없고 소수라면
            if n not in primes and prime(n):
                primes.append(n)
    
    return len(primes)


def prime(num):
    if num < 2:
        return False
    div = 2
    while div <= num//2:
        if num % div == 0:
            return False
        div += 1
    return True
```
