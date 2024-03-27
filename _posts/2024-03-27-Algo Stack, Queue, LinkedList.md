---
title: Algo Stack, Queue, LinkedList
date: 2024-03-27 22:03 +0900
categories: Algorithm
tags:
  - Python
  - CodingTest
  - 자료구조
---
# Intro
---
백준에서 문제를 풀이하다 Stack, Queue, LinkedList에 관한 문제를 접하면서 예전에 한번 공부했던 내용이지만 다시한번 정리하고자 각 자료구조들은 무엇이고 파이썬으로 구현하는 방법에대해서 정리해 보려고 한다.

## 자료구조 
---
자료구조는 크게 나누면 아래와 같다.

1. 단순 구조(Primitive Data Structure or Base Data Structure)
2. 선형 구조(Linear Data Structure)
3. 비선형 구조(Non-Linear Data Structure))
4. 파일 구조(File Organization)

>단순 구조는 우리가 프로그래밍을 하며 흔히 사용하는 정수, 실수, 문자, 문자열과 같이 프로그래밍 언어에서 제공하는 기본적인 자료형을 뜻한다.

>선형 구조는 각각의 자료들 사이의 앞뒤 관계가 일대일(1:1)인 경우를 뜻하며 대표적으로는 리스트(List), 스택(Stack), 큐(Queue) 등이 있다.

>비선형 구조는 각각의 자료들 사이의 앞뒤 관계가 일대일이 아닌 계층 구조(Hierarchical Strucure) 또는 망 구조(Network Structure)를 가지는 경우가 많으며 트리(Tree) 와 그래프(Graph)가 대표적이다

>파일구조는 보조기억장치(ex)HDD)에 저장되는 파일에 대한 자료구조를 뜻하며 선형, 비선형 자료구조가 컴퓨터 메모리상에 저장된다는 가정에 의한 것이라면 파일구조는 메모리가 아니라 디스크에 저장된다는 가정을 기반에 두었기 때문에 메모리에 올릴수없는 대용량의 자료들을 대상으로한다. 
>대표적으로 순차적 파일 구조(Sequential), 상대적 파일 구조(Relative), 색인 파일구조(Indexed Sequential), 다중 키 파일 구조(Multi-Key) 등이있다.


---

### List
---

>리스트는 자료를 순서대로 저장하는 자료구조로 단순해서 가장 많이 사용된다고 할 수 있다.
여러개의 자료가 일직선으로 서로 연결된 (Sequential) 선형구조를 의미한다.

파이썬에서는 대괄호([ ])와 쉼표(,)를 사용해서 간단하게 표현가능하다.

```python
리스트명 = [요소1, 요소2, 요소3, ...]
a = list() # 비어있는 리스트는 이런식으로 생성할 수 있다.
```

	리스트도 문자열과 같이 인덱싱과 슬라이싱이 가능하다.
### Stack
---
>스택은 가장 나중에 넣은 데이터를 가장 먼저 꺼내쓸 수 있는 데이터구조로 흔히 LIFO(Last In First Out)라고 한다. 파이썬으로 스택을 구현할때는 연결리스트를 만드는 것처럼 리스트를 사용해서 만들수 있다.

```python
li = list() #[]
li.append(1) # 리스트 맨 뒤에 1 추가
=> [1]

li.append(2) # 리스트 맨 뒤에 2 추가
li.append(3) # 리스트 맨 뒤에 3 추가
=> [1,2,3]

li.pop() # 리스트 맨 뒤 요소 꺼내고 리스트에서 삭제
=>[1,2]
```

클래스를 이용해서 직접 구현하면 다음과 같다

```python
class stack: 
	def __init__(self): # 스택 객체 생성 
		self.items = [] 
	
	def push(self, item): # 스택 요소 추가 push(.append()) 
		self.items.append(item) 
	
	def pop(self): # 스택 맨 뒤 요소 삭제하고 리턴 pop() 
		return self.items.pop() 
	
	def peek(self): # 스택 맨 뒤 요소 리턴 
		return self.items[-1] 
	
	def isEmpty(self): # 스택이 비었는지 확인(비었으면 True 리턴) 
		return not self.items

```

### Queue
---
>큐 는가장 먼저넣은 데이터를 가장 먼저 꺼내쓸 수 있는 데이터구조로 흔히 FIFO(First In First Out) 또는 선입선출 이라고 한다. 

파이썬으로 큐를 구현할때는 스택을 만드는 것과 비슷하게 리스트를 사용해서 만들수 있다.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear = None

    def enqueue(self, data):
        if self.front is None:
            self.front = self.rear = Node(data)
        else:
            node = Node(data)
            self.rear.next = node
            self.rear = node

    def dequeue(self):
        if self.front is None:
            return None
        node = self.front
        if self.front == self.rear:
            self.front = self.rear = None
        else:
            self.front = self.front.next
        return node.data

    def is_empty(self):
        return self.front is None

if __name__ == "__main__":
    q = Queue()

    for i in range(3):
        q.enqueue(chr(ord("A") + i))
        print(f"Enqueue data = {q.rear.data}")
    print()

    while not q.is_empty():
        print(f"Dequeue data = {q.dequeue()}")
```

### LinkedList
---
>연결 리스트는 데이터를 연속된 메모리 공간에 저장하지 않고, 각 데이터가 다음 데이터의 위치를 가리키는 형태로 구성된 선형 자료 구조다. 각 데이터 단위를 노드라고 하며, 노드는 데이터와 함께 다음 노드를 가리키는 참조(주소)를 저장한다.

노드는 값과 다음 노드의 주소(참조)를 저장하며, 연결 리스트의 시작을 의미하는 head는 첫 번째 노드의 주소를 가리킨다. 

파이썬으로 구현시 다음과 같다.
```python
class Node:
    def __init__(self, data):
        self.data = data  #data는 값을 가리키는 변수(속성, attribute)
        self.next = None  #next는 다음 노드를 가리키는 변수

head = Node(1)
head.next = Node(2)
head.next.next = Node(3)
```

배열은 인덱싱(indexing)으로 원소에 쉽게 접근할 수 있다. 그러나 원소를 추가하거나 삭제하려면, 연속한 메모리 공간을 확보하고 원소를 이동시켜야 하므로 시간이 걸린다. 그래서 자료의 양이 정해져 있지 않거나, 자료를 추가하거나 삭제하는 일이 많다면 연결 리스트가 적합하다고한다.

### 연결 리스트의 특징

- **동적 배열**: 크기를 동적으로 조절할 수 있다.
- **삽입과 삭제의 용이성**: 시작점이나 중간에 새로운 노드를 추가하거나 기존 노드를 제거하는 것이 배열에 비해 간단하고 효율적이다.
- **스택과 큐 구현에 적합**: 스택과 큐 등의 자료 구조 구현에 자주 사용한다.

### Reference
---
