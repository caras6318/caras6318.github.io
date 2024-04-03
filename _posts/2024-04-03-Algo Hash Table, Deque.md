---
title: Algo Hash Table, Deque
date: 2024-04-03 22:04 +0900
categories: Algorithm
tags:
  - 자료구조
  - Python
---
## Hash Table
---
### **[ HashTable(해시테이블)이란? ]**

해시 테이블은 (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠르게 데이터를 검색할 수 있는 자료구조이다. 해시 테이블이 빠른 검색속도를 제공하는 이유는 내부적으로 배열(버킷)을 사용하여 데이터를 저장하기 때문이다. 해시 테이블은 각각의 Key값에 해시함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색하게 된다. 여기서 실제 값이 저장되는 장소를 버킷 또는 슬롯이라고 한다.

1. key가 존재하는지 확인 (in 연산자)

```python
student_info = {} 

student_info[2024390] = "카리나" 
student_info[2024392] = "아이유" 
student_info[2024393] = "장원영" 
student_info[2024401] = "차은우" 

if 2024390 in student_info: 
	print("학생이 존재합니다") 
else: 
	print("학생이 존재하지 않습니다")

```

2. key와 value 모두 접근(dictionary.items())
   
```python
for student_id, name in student_info.items(): 
	print(student_id, name) 
	
> 2024390 카리나
> 2024392 아이유
> 2024393 장원영
> 2024401 차은우

```


3. key만 접근(dictionary.keys())
   
```python
for student_id in student_info.keys(): 
	print(student_id) 

> 2024390
> 2024392 
> 2024393 
> 2024401

```
​
4. value에만 접근(dictionary.values())

```python
for name in student_info.values(): 
	print(name) 

> 카리나
> 아이유
> 장원영
> 차은우
```

5. key에 해당하는 value을 가져오기(dictionary.get())
   
```python
print(student_info.get(2024390)) 

> 카리나
```

## Deque
---
보통 큐(queue)는 선입선출(FIFO) 방식으로 작동한다. 
반면, **양방향 큐**가 있는데 그것이 바로 **디큐(deque)**다.

즉, **앞, 뒤 양쪽 방향에서 엘리먼트(element)를 추가하거나 제거할 수 있다.**

디큐는 양 끝 엘리먼트의 append와 pop이 압도적으로 빠르다.

컨테이너(container)의 양끝 엘리먼트(element)에 접근하여 삽입 또는 제거를 할 경우, **일반적인 리스트(list)가 이러한 연산에 O(n)이 소요되는 데 반해, 디큐(deque)는 O(1)**로 접근 가능하다.

```python
from collections import deque 

# 덱 생성 
my_deque = deque() 

# 덱에 값 추가 
my_deque.append(1) # 오른쪽에 추가 
my_deque.appendleft(2) # 왼쪽에 추가 

# 덱에서 값 삭제 
my_deque.pop() # 오른쪽에서 삭제 
my_deque.popleft() # 왼쪽에서 삭제 

# 덱의 크기 
size = len(my_deque) 

# 덱 출력 
print(my_deque)

```

위의 명령어들 말고도 대표적으로 사용되는 명령어는 다음과 같다.

- `deque.append(item)`: item을 디큐의 오른쪽 끝에 삽입한다.
- `deque.appendleft(item)`: item을 디큐의 왼쪽 끝에 삽입한다.
- `deque.pop()`: 디큐의 오른쪽 끝 엘리먼트를 가져오는 동시에 디큐에서 삭제한다.
- `deque.popleft()`: 디큐의 왼쪽 끝 엘리먼트를 가져오는 동시에 디큐에서 삭제한다.
- `deque.extend(array)`: 주어진 배열(array)을 순환하면서 디큐의 오른쪽에 추가한다.
- `deque.extendleft(array)`: 주어진 배열(array)을 순환하면서 디큐의 왼쪽에 추가한다.
- `deque.remove(item)`: item을 디큐에서 찾아 삭제한다.
- `deque.rotate(num)`: 디큐를 num만큼 회전한다(양수면 오른쪽, 음수면 왼쪽).
- `deque.clear()` : 디큐 전체를 비워 length = 0으로 만든다
- `deque.copy()`: 디큐 전체를 카피
- `deque.count(x)` : x가 덱에서 몇 번이나 나타나는 지 셈
- `deque.index(x [start [, stop]])` : start와 stop 사이에서 x의 위치를 반환
- `deque.insert(x, i)` : x를 i인덱스에 삽입
- `deque.reverse()` : 원소의 순서를 in-place 역순으로 바꿈
- `deque.maxlen` : 디큐의 최대 사이즈.

다른 Queue 나 Stack과는 다른점이 마지막에 설명되어있는 rotate() 메서드이다.
```python
# Contain 1, 2, 3, 4, 5 in deq
deq = deque([1, 2, 3, 4, 5])

deq.rotate(1)
print(deq)

> deque([5, 1, 2, 3, 4])

deq.rotate(-1)
print(deq)

> deque([1, 2, 3, 4, 5])
```

Parameter 값으로 주어진 숫자만큼 디큐를 좌,우회전 시킬수 있다.

요약하자면, 디큐(deque)는 Stack 처럼 사용할 수도 있고, Queue 처럼 사용할 수도 있다.

시작점의 값을 넣고 빼거나, 끝 점의 값을 넣고 빼는 데 최적화된 연산 속도를 제공한다.

즉, 대부분의 경우에 디큐(deque)는 리스트(list)보다 월등한 옵션이다.

디큐는 특히 push/pop 연산이 빈번한 알고리즘에서 리스트보다 월등한 속도를 자랑한다.
### Reference
---
[Leon TechBlog](https://chaewonkong.github.io/posts/python-deque.html)
[Python Deque Doc](https://docs.python.org/3/library/collections.html#collections.deque)
[망나니개발자님의 TechBlog](https://mangkyu.tistory.com/102)

