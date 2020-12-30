---
title: "다시 시작하는 코딩: Problem-09"
date: 2020-12-30 20:44:39 -0400
categories: [ 프로그래머스 ]
tags: [ 스택/큐 ]
---

다리를 지나는 트럭: https://programmers.co.kr/learn/courses/30/lessons/42583

접근방법
--------
처음에는 다리 위의 상태를 나타내기 위해 다리 길이만큼의 리스트를 생성하여 관리하고자 했다. 하지만 공간 낭비가 심했기에,
어떻게 하면 다리위에 있는 트럭들이 지나갈때 까지의 시간을 쉽게 계산할지 고민했다.<br>
결론적으로 다리위에 존재하는 트럭들을 나타내는 리스트 `onbridge`와 해당 트럭들의 남은 시간을 나타내는 시간 `time` 리스트를
생성하여 관리하였다.<br><br>
**문제 조건에 따르면 트럭이 다리 위에서 보내는 시간은 모두 같고, 트럭끼리의 추월은 불가능하다.**<br>
그렇기에 리스트를 2개 만들어 다음 올라탈 트럭의 무게를 견딘다면 다리위에 트럭을 올리고 아니라면 1초씩 진행시킨다.
그리고 모든 트럭이 다리위에 올라서면 *while* 루프를 빠져나와 마지막 트럭이 지나기까지의 시간, **즉 다리 길이만큼을 다시 더해준다.**

전체 소스코드
------
```python
def solution(bridge_length, weight, truck_weights):
    answer = 0
    onbridge = []
    time = []
    trucks = len(truck_weights)
        
    while len(truck_weights):
        # 다음 트럭 무게를 견딘다면
        if weight >= sum(onbridge) + truck_weights[0]:
            onbridge.append(truck_weights.pop(0)) # pop new truck
            time.append(bridge_length)
        # next tick
        process(onbridge, time)
        answer += 1
    answer += bridge_length
    return answer

def process(bridge, time):
    for i in range(len(time)):
        time[i] -= 1
    # 맨앞 트럭이 다리를 지난지 확인
    if time[0] < 1:
        bridge.pop(0)
        time.pop(0)
```
