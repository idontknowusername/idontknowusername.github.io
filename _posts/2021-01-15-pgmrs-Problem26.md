---
title: "Problem-26: 올바른 괄호"
date: 2021-01-15 21:49:16 -0400
categories: [ 프로그래머스 ]
tags: [ 연습문제 ]
---

올바른괄호: https://programmers.co.kr/learn/courses/30/lessons/12909

문제 설명
--------
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

+ ()() 또는 (())() 는 올바른 괄호입니다.
+ )()( 또는 (()( 는 올바르지 않은 괄호입니다.

'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

제한사항
--------
+ 문자열 s의 길이 : 100,000 이하의 자연수
+ 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

 
입출력 예
-------

|s|answer|
|------|---|
|"()()"|true|
|"(())()"|true|
|")()("|false|
|"(()("|false|

접근방법
--------
1. 처음 시도한 방법은 가장 정석적인 stack을 이용한 방법이다.

> 입력받은 s를 앞에서부터 확인하면서 `'('`이면 스택에 넣고 `')'`면 스택에 들어간 `'('`를 빼준다.

```python
def solution(s):
    answer = True
    string = list(s)
    stack = []

    while len(string):
        token = string.pop(0)
        if token == '(':
            stack.append(token)
        elif token == ')' and len(stack):
            stack.pop()
        else:
            return False
    if len(stack):
        answer = False
    return answer
```

간단하게 테스트케이스는 통과했지만 효율성 테스트 2가지를 실패했다.
Big Oh notation 자체는 맞지만 쓸모없는 pop 연산을 하나라도 없애기 위해 반복문 조건을 바꿔주었다.


전체 소스코드
------
```python
def solution(s):
    answer = True
    stack = []

    for i in s:
        if i == '(':
            stack.append(i)
        elif i == ')' and len(stack):
            stack.pop()
        # stack이 비었는데 ')' 가 나온경우
        else:
            return False
    if len(stack):
        answer = False
    return answer
```
