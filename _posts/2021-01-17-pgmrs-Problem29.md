---
title: "Problem-29: 삼각달팽이"
date: 2021-01-17 18:31:28 -0400
categories: [ 프로그래머스 ]
tags: [ 월간 코드 챌린지 ]
---

삼각달팽이: https://programmers.co.kr/learn/courses/30/lessons/68645

문제 설명
--------
정수 n이 매개변수로 주어집니다. 다음 그림과 같이 밑변의 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 return 하도록 solution 함수를 완성해주세요.

![입출력](/assets/img/problem29/1.png)

제한사항
--------
+ n은 1 이상 1,000 이하입니다.

 
입출력 예
-------

|n|result|
|------|---|
|4|[1,2,9,3,10,8,4,5,6,7]|
|5|[1,2,12,3,13,11,4,14,15,10,5,6,7,8,9]|
|6|[1,2,15,3,16,14,4,17,21,13,5,18,19,20,12,6,7,8,9,10,11]|

접근방법
--------
1. 입력값 `n` 만큼의 2차원 배열을 만든다.
2. 아래 -> 오른쪽 -> 대각선 순서대로 끝을 만날때까지 진행하면서 1씩 더해진 값을 넣는다.
3. 완성된 배열을 초기화 값을 제외하고 전부 출력해준다.

전체 소스코드
------
```python
def solution(n):
    answer = []
    two = []
    
    # initial value with -1
    for i in range(n+2):
        two.append([-1]*(n+2))
    
    # initial value with 0
    for i in range(1,n+1):
        for j in range(1,n+1):
            if i >= j:
                two[i][j] = 0
    total = 0
    for i in range(n+1):
        total += i
    
    # initial cursor
    cur = 1
    row = 1
    col = 1
    # 0: 아래
    # 1: 오른쪽
    # 2: 대각선
    direction = 0
    
    while True:
        two[row][col] = cur
        cur += 1
        
        # Exit condition
        if cur > total:
            break
        
        # direction
        if direction == 0:
            if two[row+1][col] == 0:
                row += 1
            else:
                col += 1
                direction = 1
        elif direction == 1:
            if two[row][col+1] == 0:
                col += 1
            else:
                row -= 1
                col -= 1
                direction = 2
        elif direction == 2:
            if two[row-1][col-1] == 0:
                row -= 1
                col -= 1
            else:
                row += 1
                direction = 0
    
    # formating
    for i in range(1,n+1):
        for j in range(1,n+1):
            if two[i][j] != -1:
                answer.append(two[i][j])
            #print('{} '.format(two[i][j]), end = '')
        #print()
    
    #print(answer)
    return answer
```
