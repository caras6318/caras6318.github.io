---
title: 99클럽 코테 스터디 8일차 TIL - JAVA Queue
date: 2024-07-29 23:07 +0900
categories: JAVA
tags:
  - 99클럽
  - 개발자취업
  - 자료구조
  - 코딩테스트준비
  - 항해99
---
## Intro
---
항해99 코딩테스트 스터디를 진행하면서 저번주 문자열에 이어서 이번주에는 스택/큐가 주제로 정해졌다. 이번 기회에 JAVA에서 Queue를 사용하는 방법에 대해서 정리해 보려고 한다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

![logo](/assets/img/basic99.png)

## Queue
---
Java에서는 다양한 Queue 인터페이스와 그 구현체들을 제공한다. 각각의 Queue 구현체는 특정한 특성을 가지고 있어서, 상황에 따라 적합한 것을 선택하여 사용할 수 있다.

Java에서는 Queue 인터페이스와 다음과 같은 구현체를 제공한다.
1. LinkedList
2. ArrayDeque
3. PriorityQueue
### 1. Queue 인터페이스
---
java.util.Queue 인터페이스는 FIFO(First-In-First-Out) 방식의 데이터 구조를 정의한다.

• 주요 메서드: add, offer, remove, poll, element, peek 등
• 일반적으로 LinkedList나 ArrayDeque와 같은 구현체로 사용된다.

직접 인테페이스를 확인해보니 비슷한 기능을 하는데 다른 메서드를 사용한다는걸 알 수 있었다.

1. Insert (삽입)

- add(e) :  요소를 큐의 끝에 추가하며, 만약 공간이 부족하면 IllegalStateException을 발생시킨다.

```java
Queue<Integer> queue = new LinkedList<>();
queue.add(1);
queue.add(2);
```
- offer(e) : 요소를 큐의 끝에 추가하며, 만약 공간이 부족하면 false를 반환한다.
```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(1);
queue.offer(2);
```

두 메서드는 Queue에 공간이 부족하면 예외를 반환하냐, false를 반환하냐의 차이가 있다.

2. Remove (제거)

- remove() : 큐의 처음 요소를 제거하며, 큐가 비어있으면 NoSuchElementException을 발생시킨다.
```java
Queue<Integer> queue = new LinkedList<>();
queue.add(1);
queue.add(2);
queue.remove(); // 1을 제거하고 반환
```
- poll() : 큐의 처음 요소를 제거하며, 큐가 비어있으면 null을 반환한다.
```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(1);
queue.offer(2);
queue.poll(); // 1을 제거하고 반환
```

두 메서드는 Queue가 비어있을 때 예외를 반환하냐, false를 반환하냐의 차이가 있다.

3.Examine (조사)

- element() : 큐의 처음 요소를 반환하며, 큐가 비어있으면 NoSuchElementException을 발생시킨다. 
```java
Queue<Integer> queue = new LinkedList<>();
queue.add(1);
queue.add(2);
int first = queue.element(); // 큐의 첫 번째 요소를 반환 (1)
```
- peek() : 큐의 처음 요소를 반환하며, 큐가 비어있으면 null을 반환한다.
```java
Queue<Integer> queue = new LinkedList<>();
queue.offer(1);
queue.offer(2);
int first = queue.peek(); // 큐의 첫 번째 요소를 반환 (1)
```

두 메서드는 Queue가 비어있을 때 예외를 반환하냐, false를 반환하냐의 차이가 있다.
### 2. LinkedList
---
java.util.LinkedList는 Queue 인터페이스를 구현한 클래스로, 노드 기반의 양방향 연결 리스트이다.

• 큐의 처음과 끝에서 데이터를 추가하거나 제거할 수 있다.
• 큐 외에도 리스트나 데크(Deque) 등으로 활용할 수 있다.

### 3. ArrayDeque
---
java.util.ArrayDeque는 큐와 데크(Deque)를 구현한 클래스로, 배열 기반의 큐이다.

• 큐의 양쪽 끝에서 데이터를 추가하거나 제거할 수 있다.
• 높은 성능을 제공하며 큐와 스택을 모두 구현할 수 있다.

### 4. PriorityQueue
---
java.util.PriorityQueue는 우선순위 큐를 구현한 클래스이다.

• 우선순위에 따라 요소들이 정렬되어 저장되며, 최소 힙(Min Heap) 구조를 기반으로 한다.
• 가장 우선순위가 높은 요소를 먼저 제거한다.

### Reference
---
