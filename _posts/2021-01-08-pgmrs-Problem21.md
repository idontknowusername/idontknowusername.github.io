---
title: "다시 시작하는 코딩: Problem-21"
date: 2021-01-08 22:15:23 -0400
categories: [ 프로그래머스 ]
tags: [ Greedy ]
---

조이스틱: https://programmers.co.kr/learn/courses/30/lessons/42860

문제 설명
--------
조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.
```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동
```
예를 들어 아래의 방법으로 JAZ를 만들 수 있습니다.
```
- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
```
만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

제한사항
--------
+ name은 알파벳 대문자로만 이루어져 있습니다.
+ name의 길이는 1 이상 20 이하입니다.

 
입출력 예
-------

|name|return|
|------|---|
|"JEROEN"|56|
|"JAN"|23|

접근방법
--------
1. `cur` 리스트를 생성해 조건을 맞췄다면 0, 아니라면 1로 처리해준다
2. 0번 인덱스에서 출발해 해당 인덱스의 원소가 조건을 맞출때까지의 조작횟수를 더한다.
3. **A가 아닐때까지 왼쪽과 오른쪽으로 각각 점프 후 더 적게 움직여야 하는 곳으로 인덱스를 옮긴다.**
4. 모든 원소가 조건을 맞출때까지 반복한다.

전체 소스코드
------
```python
def solution(name):
    answer = 0
    cur = []
    length = len(name)
    
    # 이미 A라면 0 아니면 1
    for i in range(length):
        cur.append(0 if name[i] == 'A' else 1)
    
    # 종료조건용 변수
    condition = sum(cur)
    idx = 0
    while True:
        # 해당 슬롯이 완성이 안됐다면
        if cur[idx]:
            # 알파벳 거리 추가 후, 0으로
            answer += get_diff(name[idx])
            cur[idx] = 0
            condition -= 1
        
        # 모두 완료되면 종료
        if not condition:
            break
            
        # 왼쪽 오른쪽으로 점프
        left = 1
        right = 1
        while cur[(idx-left) % length] == 0:
            left += 1
        while cur[(idx+right) % length] == 0:
            right += 1
        # 왼쪽이 더 적게 간다면
        if left < right:
            answer += left
            idx = (idx-left) % length
            print('left ' ,left)
        # 오른쪽이 더 적게 간다면
        else:
            answer += right
            idx = (idx+right) % length
            print('right ' ,right)
    return answer

def get_diff(char):
    direction = ord(char) - ord('A')
    # 아스키코드의 차가 13(N)이상이면 반대방향으로
    if direction > 13:
        return 26 - direction
    # 아니라면 정방향으로
    else:
        return direction
```
