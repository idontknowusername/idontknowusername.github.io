---
title: "다시 시작하는 코딩: Problem-07"
date: 2020-12-30 18:09:46 -0400
categories: [ 프로그래머스 ]
tags: [ 스택/큐 ]
---

주식가격: https://programmers.co.kr/learn/courses/30/lessons/42584

접근방법
--------
입력값 prices 배열을 linear하게 탐색한다. answer 배열의 각 원소들의 초기화 값은
`전체배열길이 - 인덱스번호 - 1`
![초기화](/assets/img/problem7/1.png)
이며 이것은 순차적으로 탐색하면서 해당 가격보다 낮은 가격이 안나올 경우 갖게 되는 return 값이다.
![초기화](/assets/img/problem7/2.png)
만약 탐색하는 도중 최초로 원래 가격보다 낮은 가격이 나올경우
![초기화](/assets/img/problem7/3.png)
인덱스 번호 **j**에서 원래 가격의 인덱스 번호인 **i**를 빼준 값을 넣어준다.
![초기화](/assets/img/problem7/4.png)

전체 소스코드
------
```python
def solution(prices):
    answer = []
    length = len(prices)
    for i in range(length):
        answer.append(length-i-1)
        for j in range(i,length):
            if prices[i] > prices[j]:
                answer[i] = j - i
                break
    
    return answer
```
