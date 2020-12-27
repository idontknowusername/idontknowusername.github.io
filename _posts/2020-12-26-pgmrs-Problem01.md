---
title: "다시 시작하는 코딩: Problem-01"
date: 2020-12-26 13:30:28 -0400
categories: [ 프로그래머스 ]
tags: [ 해시] 
---

완주하지 못한 선수: https://programmers.co.kr/learn/courses/30/lessons/42576?language=python3

최초접근
--------
처음 작성한 코드는
```python
def solution(participant, completion):
    answer = ''
    for i in range(len(completion)):
        participant.remove(completion[i])
    answer = participant[0]
    return answer
```
단순히 참가자 배열에서 완주한 선수를 remove 메소드를 이용하여 제거하는 코드였다.
하지만 remove 메소드가 결국 linear search를 이용한 방법이기 때문에
이 방법은 O(n<sup>2</sup>)의 시간복잡도를 가졌고, 효율성 검사에서 전부 실패하였다.
따라서 **Sorting**을 통해 시간복잡도를 줄이고자 하였다.

해법
------
참가자와 완주 선수 배열을 각자 abc 순서대로 정렬하고 나면<br>
participant: `['a','b','c','d','e','e','f','g','h']`<br>
completion:  `['a','b','c','d','e','f','g','h']`<br>
이런 식으로 같은 인덱스에서 서로 매칭되는 선수들이 나오게 된다.
두 배열을 0번 인덱스부터 linear하게 비교한다면, 처음으로 일치하지 않는 인덱스가
곧 완주하지 못한 선수를 의미하게 되고, 만약 마지막 루프까지 돌아도 일치하지 않는 인덱스를
발견하지 못했다면 곧 participant 배열의 마지막 사람이 완주하지 못한 사람임을 의미한다.
```python
def solution(participant, completion):
    answer = ''
    participant.sort()
    completion.sort()
    for i in range(len(completion)):
        if participant[i] == completion[i]:
            continue
        else:
            answer = participant[i]
            break # 답을 찾은 뒤 break로 빠져나와야 함
    if answer == '':
        answer = participant[len(participant)-1]
    return answer
```
