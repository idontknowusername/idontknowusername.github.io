---
title: "다시 시작하는 코딩: Problem-22"
date: 2021-01-11 13:41:58 -0400
categories: [ 프로그래머스 ]
tags: [ Greedy ]
---

큰 수 만들기: https://programmers.co.kr/learn/courses/30/lessons/42883

문제 설명
--------
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

제한사항
--------
+ number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
+ k는 1 이상 `number의 자릿수` 미만인 자연수입니다.

 
입출력 예
-------

|number|k|return|
|------|---|---|
|"1924"|2|"94"|
|"1231234"|3|"3234"|
|"4177252841"|4|"775841"|

접근방법
--------
1. 스택을 생성해서 입력값 `number`의 값들을 다음 조건에 맞춰 스택에 넣는다.
  + 스택이 비어있지 않아야한다.
  + 스택의 마지막 숫자가 입력값보다 작아야한다.
  + 아직 숫자를 주어진 `k`보다 덜 제거했다면
  + pop 한뒤 push 한다.(스택의 마지막을 대체한다)


전체 소스코드
------
```python
def solution(number, k):
    answer = ''
    # stack 생성
    stack = [number[0]] #[0]
    
    # number값을 앞에서부터 차례대로 입력
    for num in number[1:]:
        # 1. 스택이 비어있지 않고,
        # 2. 스택의 마지막 숫자가 입력값보다 작고,
        # 3. 아직 뺄 숫자가 남았다면,
        while len(stack) > 0\
        and stack[-1] < num\
        and k > 0:
            # 4. 마지막 숫자를 뺀다
            k -= 1
            stack.pop()
        # 5. 새로 들어온 숫자를 스택에 쌓는다
        stack.append(num)
        
    if k != 0:
        stack = stack[:-k]
        
    answer = answer.join(stack)
    return answer
```
