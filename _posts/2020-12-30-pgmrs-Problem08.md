---
title: "다시 시작하는 코딩: Problem-08"
date: 2020-12-30 18:25:55 -0400
categories: [ 프로그래머스 ]
tags: [ 스택/큐 ]
---

기능개발: https://programmers.co.kr/learn/courses/30/lessons/42586

접근방법
--------
앞쪽 기능이 개발된 상태여야 뒤쪽의 작업도 동시에 진행되기 때문에 앞에서부터 순서대로 스캔한다.
*cur* 변수는 현재 완료되지 않은 맨 앞 작업을 가르키며, 모든 작업이 완료될때 까지 반복문을 돌린다.<br>
가르키고 있는 맨 앞의 미완료 작업이 완료 되지 않았다면 하루의 작업을 수행하고, 만약 완료된 상태라면 이후 연속된 작업들이 있는지 확인 후,
완료된 작업의 수 *count*가 그날 완료된 모든 작업의 숫자기 때문에 *answer* 배열에 추가해주고, 완료된 작업의 수만큼 *cur* 인덱스 번호도 밀어준다.

전체 소스코드
------
```python
def solution(progresses, speeds):
    answer = []
    cur = 0
    ends = len(progresses)
    
    while cur < ends:
        # 맨앞 작업이 완료됐다면
        if progresses[cur] >= 100:
            count = 1
            # 이후에 연속된 작업들이 완료된지 확인
            for i in range(cur + 1, ends):
                if progresses[i] >= 100:
                    count += 1
                else:
                    break
            answer.append(count)
            cur += count
        else:
            # 하루의 작업 수행
            for i in range(len(progresses)):
                progresses[i] += speeds[i]
    
    return answer
```
