---
title: "다시 시작하는 코딩: Problem-18"
date: 2021-01-05 12:12:36 -0400
categories: [ 프로그래머스 ]
tags: [ 연습문제 ]
---

124 나라의 숫자: https://programmers.co.kr/learn/courses/30/lessons/12899

문제 설명
--------
문제 설명
124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.

1. 124 나라에는 자연수만 존재합니다.
2. 124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.

예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.

![예](/assets/img/problem18/1.png)

자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

제한사항
--------
+ n은 500,000,000이하의 자연수 입니다.

입출력 예
-------
![입출력](/assets/img/problem18/2.png)

접근방법
--------
1. 0부터 3진수로 치환한다. 1은 0이 되고, 2는 1이 되고, 4는 2로 사용한다.
2. 3진수로 전환하기전 1씩 빼줘서 자리수를 맞춰준다.

전체 소스코드
------
```python
def solution(n):
    answer = ''
    # 0부터 3진수로 치환
    # 1 = 0
    # 2 = 1
    # 4 = 2
    num = ['1','2','4']
    
    while n:
        n -= 1
        answer = num[n % 3] + answer
        n = n//3
        
    return answer
```