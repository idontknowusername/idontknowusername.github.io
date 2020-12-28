---
title: "다시 시작하는 코딩: Problem-03"
date: 2020-12-28 14:05:07 -0400
categories: [ 프로그래머스 ]
tags: [ 해시 ]
---

전화번호 목록: https://programmers.co.kr/learn/courses/30/lessons/42579
O(2<sup>n</sup>)

접근방법
--------
각 genres 배열을 순차적으로 탐색하면서 2차원 배열 **array**에다가
> [[장르1, 총 재생횟수, 재생횟수1, 재생횟수2, 재생횟수3], [장르2, 총 재생횟수, 재생횟수1, 재생횟수2], ...]

형식으로 된 테이블을 생성한다.<br>
즉, array[i][0]은 중복되지 않는 각 장르를 나타내고,
array[i][1]은 해당 장르의 총 재생횟수를 나타낸다.<br<
다음으로 만들어진 2차원 배열 테이블을 총 재생횟수를 lambda 값으로 내림차순 정렬하여
총 재생횟수가 많은 장르를 앞에 오게 만든다.
```python
for i in range(len(genres)):
    # 최초 loop는 정적으로 입력해준다.
    if not len(array):
        array.append([genres[0], plays[0], plays[0]])
        continue
    for j in range(len(array)):
        # 전에 나온 장르라면
        if genres[i] == array[j][0]:
            array[j].append(plays[i])
            array[j][1] += plays[i]
            break
        # 나온적 없는 장르라면
        if j == (len(array) - 1):
            array.append([genres[i], plays[i], plays[i]])
            break
array.sort(key=lambda total:total[1], reverse = True)
```
(정렬한 이미지)

하지만 여기까지 만들어진 배열로는 최초의 인덱스(고유번호)를 추적할 수 없기 때문에 고유번호를 추가해서
배열을 바꾼다. 상당히 억지로 만든 느낌이 없지않아 있지만 지금까지 배열을 정리한다면
> array 배열: [[장르, 총 재생횟수,[[재생횟수, 고유번호],[재생횟수, 고유번호],[재생횟수, 고유번호]]], ...]

이런식으로 4차원 배열까지 들어가게 된다...~~미친놈~~<br>
사실상 배열을 가지고 일종의 데이터그램을 만든것이고 이 배열의 키 값을 조건에 맞춰 적절히 정렬하면 순서대로 인덱스 번호를 출력시키면 된다.

전체 소스코드
------
```python
def solution(genres, plays):
    answer = []
    array = []
    for i in range(len(genres)):
        # 최초 loop는 정적으로 입력해준다.
        if not len(array):
            array.append([genres[0], plays[0], [[plays[0], 0]]])
            continue
        for j in range(len(array)):
            # 전에 나온 장르라면
            if genres[i] == array[j][0]:
                array[j][2].append([plays[i], i])
                array[j][1] += plays[i]
                break
            # 나온적 없는 장르라면
            if j == (len(array) - 1):
                array.append([genres[i], plays[i], [[plays[i], i]]])
                break
    array.sort(key=lambda total:total[1], reverse = True)
    
    # 각 인덱스 번호 내림차순 정렬
    for i in range(len(array)):
        array[i][2].sort(reverse = True, key=lambda x:(x[0],-x[1]))
    
    for i in range(len(array)):
        answer.append(array[i][2][0][1])
        # 장르에 해당하는 노래가 하나밖에 없다면 다음 루프로
        if len(array[i][2]) == 1:
            continue
        answer.append(array[i][2][1][1])
    print(array)
    return answer
```
