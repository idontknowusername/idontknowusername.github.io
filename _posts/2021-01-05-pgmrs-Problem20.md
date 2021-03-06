---
title: "다시 시작하는 코딩: Problem-20"
date: 2021-01-05 17:52:34 -0400
categories: [ 프로그래머스 ]
tags: [ Greedy ]
---

체육복: https://programmers.co.kr/learn/courses/30/lessons/42862

문제 설명
--------
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.


제한사항
--------
+ 전체 학생의 수는 2명 이상 30명 이하입니다.
+ 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
+ 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
+ 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
+ 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

 
입출력 예
-------

|n|lost|reserve|return|
|------|---|---|---|
|5|[2,4]|[1,3,5]|5|
|3|[2,4]|[3]|4|
|3|[3]|[1]|2|

접근방법
--------
1. 학생수 길이 + 2의 크기를 가진 리스트를 모든 원소값 1로 생성한다.
2. `lost`와 `reserve`리스트의 원소에 해당하는 인덱스의 값을 각각 -1, +1 해준다.
3. 왼쪽, 오른쪽 순서로 비교해서 체육복을 빌려준다.
4. 체육복을 가진 학생수를 출력한다.

전체 소스코드
------
```python
def solution(n, lost, reserve):
    answer = 0
    mylist = [1] * (n+2)
    
    for i in lost:
        mylist[i] -= 1
    for i in reserve:
        mylist[i] += 1
    # 맨 앞사람과 맨 뒷사람 이웃은 1명밖에 없다
    mylist[0] = 0
    mylist[n+1] = 0
    
    # 1번부터 n번까지
    for i in range(1, len(mylist) - 1):
        # 내가 체육복이 없다면
        if not mylist[i]:
            # 이전 사람이 여벌이 있다면
            if mylist[i-1] == 2:
                mylist[i] = 1
                mylist[i-1] = 1
            # 다음 사람이 여벌이 있다면
            elif mylist[i+1] == 2:
                mylist[i] = 1
                mylist[i+1] = 1
                
    # 체육복을 가진 사람수 더하기
    for cloth in mylist:
        if cloth:
            answer+=1
    
    return answer
```
