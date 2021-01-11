---
title: "다시 시작하는 코딩: Problem-23"
date: 2021-01-11 14:36:33 -0400
categories: [ 프로그래머스 ]
tags: [ Greedy ]
---

구명보트: https://programmers.co.kr/learn/courses/30/lessons/42885

문제 설명
--------
무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.

예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

제한사항
--------
+ 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
+ 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
+ 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
+ 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

 
입출력 예
-------

|people|limit|return|
|------|---|---|
|[70,50,80,50]|100|3|
|[70,80,50]|100|3|

접근방법
--------
1. `people` 리스트를 내림차순으로 정렬한 뒤, 순서대로 pop한다.
2. 들어갈 자리가 남았다면 거기 넣고, 없다면 answer++ 한 뒤, 새 보트를 만든다.

```python
def solution(people, limit):
    answer = 0
    boats = []
    people.sort(reverse=True)   
    print(people)
    
    while len(people):
        person = people.pop(0)
        # 탑승한 보트가 없다면 추가
        if not len(boats):
            answer += 1
            boats.append(person)
            continue
        # 들어갈 자리를 찾았다면
        seat = find_seat(boats, person, limit)
        if seat != -1:
            boats[seat] += person
        else:
            answer += 1
            boats.append(person)
            
    return answer

def find_seat(boats, person, limit):
    for i in range(len(boats)):
        if (boats[i] + person) <= limit:
            return i
    return -1
```

위 방법대로 실행한 결과 테스트 케이스 3개가 실패하고, 효율성에서 모조리 실패가 뜬다. 
들어갈 자리를 찾는 과정에서 O(M×N)의 시간복잡도가 발생하기 때문인 것 같다.<br>

문제에서 중요한 것은 `구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고` 이 부분이다. 
위 코드 대로라면 빈 공간만 있다면 한 보트에 3명 이상이 타게 되고, 그 상황을 체크하기 위해 쓸데없이
`find_seat` 함수를 통해 자리를 찾도록 한 것이다. 하지만 2명까지 밖에 탈 수 없다면 다음과 같이 생각할 수 있다.

1. `people` 리스트를 내림차순으로 정렬한다.
2. 가장 무거운 사람과, 가장 가벼운 사람의 무게를 더한다.
  + 둘 다 탈 수 있다면 i,j 둘다 인덱스를 조절해서 둘다 태운다.
  + 둘 다 탈 수 없다면, i 인덱스만 조절해서 무거운 사람만 태운다.
3. 위와 같이 하는 이유는 무거운 사람이 혼자 타는 경우는 있어도 가벼운 사람이 혼자 타는 경우는 마지막에 남은 경우 말고 없기 때문이다.


전체 소스코드
------
```python
def solution(people, limit):
    answer = 0
	# 무거운 사람이 앞에 오도록 정렬
    people.sort(reverse=True)   
    
    i, j = 0, len(people) - 1
    
	# 양 끝에서 한 명씩 태울때 마다 인덱스를 가운데쪽으로 옮긴다.
	# 즉, 인덱스가 역전되면 모든 사람들을 태운 것이다.
    while i <= j:
        answer += 1
        # 가장 무거운 사람과 가벼운 사람이 같이 탈수있다면
        if people[i] + people[j] <= limit:
            # 가벼운 사람을 태우고
            j -= 1
        # 무서운 사람만 태운다.
        i += 1
        
    return answer
```
