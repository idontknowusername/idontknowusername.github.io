---
title: "Problem-33: 정수 삼각형"
date: 2021-02-19 16:47:11 -0400
categories: [ 프로그래머스 ]
tags: [ DP ]
---

정수 삼각형: https://programmers.co.kr/learn/courses/30/lessons/43105

문제 설명
--------

![입출력](/assets/img/problem33/1.png)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

제한사항
--------
+ 삼각형의 높이는 1 이상 500 이하입니다.
+ 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

 
입출력 예
-------

|triangle|result|
|------|---|
|[[7], [3, 8], [8, 1, 0], [2, 7, 4, 4], [4, 5, 2, 6, 5]]|30|

접근방법
--------
기본적인 DP 문제이다. 접근방법은 다음과 같다.

1. triangle 배열에 있는 값들을 하나씩 접근한다.
2. 해당 값이 가장 왼쪽에 있을때, 가장 오른쪽에 있을때는 부모가 하나이기 때문에 바로 더해준다.
3. 그 외의 경우에는 두 부모의 값중, 더 큰것을 더해준다.
4. 최대값을 출력한다.

전체 소스코드
------
```python
def solution(triangle):
    '''
    7
    3 8
    8 1 0
    2 7 4 4
    4 5 2 6 5
    '''

    for i in range(1, len(triangle)):
        for j in range(len(triangle[i])):
            # left side
            if j == 0:
                triangle[i][j] += triangle[i-1][j]
            # right side
            elif j == len(triangle[i]) - 1:
                triangle[i][j] += triangle[i-1][j-1]
            else:
                triangle[i][j] += max(triangle[i-1][j-1],triangle[i-1][j])
    #print(triangle)
	
    return max(triangle.pop())
```
