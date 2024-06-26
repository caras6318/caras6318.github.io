---
title: Python Comprehesions
date: 2024-04-03 21:04 +0900
categories: Python
tags:
  - Python
  - 자료구조
---
## Intro
---
컴프리헨션은 **파이썬 자료구조(list, dictionary, set)에 데이터를 좀 더 쉽고 간결하게 담기 위한 문법**이다. 
여기서 말하는 '쉽고 간결하게' 데이터를 담는 방법이란 반복문과 조건문을 결합하여 하나의 구문으로 만들어 담는 것을 의미한다.

기존에 배운 문법으로 1부터 10까지 정수를 순서대로 가지고 있는 리스트를 생성하는코드는 다음과 같다.

```python
numbers = []
for n in range(1, 10+1):
    numbers.append(n)
```

리스트를 생성하는 컴프리헨션을 리스트 컴프리헨션 이라고 부르며 아래와 같다.

```python
[x for x in range(10)]
```

컴프리헨션은 반복문과 조건문을 결합해서 다음과 같이 사용할 수 있다.

```python
[x for x in range(1, 10+1) if x % 2 == 0]

>>>[2, 4, 6, 8, 10]
```

또한 반복문과 조건문을 중첩해서 사용할 수 있다.
#### for
가능한 경우에 수를 뽑는 코드를 컴프리헨션으로 표현하면 다음과 같이 작성할 수 있습니다.

```python
[ (x, y) for x in ['쌈밥', '치킨', '피자'] for y in ['사과', '아이스크림', '커피']]

> [('쌈밥', '사과'),
 ('쌈밥', '아이스크림'),
 ('쌈밥', '커피'),
 ('치킨', '사과'),
 ('치킨', '아이스크림'),
 ('치킨', '커피'),
 ('피자', '사과'),
 ('피자', '아이스크림'),
 ('피자', '커피')]
```

이런식으로 컴프리헨션 문법은 다중 for문을 지원한다.

중복된 for문이 작동하는 순서는 왼쪽에 있는 for문이 먼저 작동을 합니다.

기존의 방식대로 for문으로 바꾼다면 다음과 같다.

```python
Copyfor x in ['쌈밥', '치킨', '피자']:
    for y in ['사과', '아이스크림', '커피']:
        for z in ['배달 시키기', '가서 먹기']:
            print(x, z, y)
```

#### if

if문 또한 중복해서 작성해서 여러 조건을 걸 수 있다.

```python
[ x for x in range(10) if x < 5 if x % 2 == 0 ]

> [0, 2, 4]
```
### Reference
---
[제대로 파이썬](https://wikidocs.net/22805)
[파이썬 기본을 갈고 닦자](https://wikidocs.net/16064)
