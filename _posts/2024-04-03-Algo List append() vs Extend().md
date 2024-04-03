---
title: Algo List append() vs Extend()
date: 2024-04-03 20:04 +0900
categories: Algorithm, Python
tags:
  - Python
  - 자료구조
---
	## Intro
---
코딩테스트를 준비하면서 여러 문제들을 풀어보고 있는중인데 List 자료구조를 사용하면서 새로운 원소를 추가하는 방법에 대해서 작성해 보려고 한다.

List 자료형에 새로운 원소를 추가하는 방법은 크게 3가지가 있다.

1. list.insert(_i_, _x_)
>리스트의 끝에 추가하는게 아니라 Index를 Parameter값으로 넣어서 원하는 위치에 삽입을 할수 있다. `a.insert(0, x)` 는 리스트의 처음에 삽입하고, `a.insert(len(a), x)` 는 `a.append(x)` 리스트의 끝에 추가한다.

2. list.append(_x_)
>리스트의 끝에 추가한다. `a[len(a):] = [x]` 와 같이도 사용할 수 있다.

3. list.extend(_iterable_)
>리스트의 끝에 이터러블의 모든 항목을 추가한다. `a[len(a):] = iterable` 와  같이도 사용할 수 있다.

```python
x = ['Tick', 'Tock', 'Song'] 
y = ['Ping', 'Pong'] 
x.append(y) 
print('x:', x) 

> x: ['Tick', 'Tock', 'Song', ['Ping', 'Pong']]

x = ['Tick', 'Tock', 'Song'] 
y = ['Ping', 'Pong'] 
x.extend(y) 
print('x:', x) 

> x: ['Tick', 'Tock', 'Song', 'Ping', 'Pong']

x = ['Tick', 'Tock', 'Song'] 
y = [['Ping', 'Pong']] 
x.append(y) 
print('x:', x) 

> x: ['Tick', 'Tock', 'Song', [['Ping', 'Pong']]]

x = ['Tick', 'Tock', 'Song'] 
y = [['Ping', 'Pong']] 
x.extend(y) 
print('x:', x) 

> x: ['Tick', 'Tock', 'Song', ['Ping', 'Pong']]

x = ['Tick', 'Tock', 'Song'] 
y = 'Ping' 
x.append(y) 
print('x:', x) 

> x: ['Tick', 'Tock', 'Song', 'Ping']

x = ['Tick', 'Tock', 'Song'] 
y = 'Ping' 
x.extend(y) 
print('x:', x)

> x: ['Tick', 'Tock', 'Song', 'P', 'i', 'n', 'g']
```




### Reference
---
[Python List Doc](https://docs.python.org/ko/3/tutorial/datastructures.html#more-on-lists)
