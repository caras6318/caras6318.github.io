---
title: 99클럽 코테 스터디 9일차 TIL - JAVA PriorityQueue
date: 2024-07-30 22:00 +0900
categories: JAVA
tags:
  - 99클럽
  - 개발자취업
  - 자료구조
  - 코딩테스트준비
  - 항해99
  - TIL
---
## Intro
---
저번 포스팅에서는 JAVA에서 제공하는 Queue 인터페이스에 대해서 알아 보았는데, 이번 포스팅에서는 구현체중 하나인 우선순위 큐 PriorityQueue에 대해서 알아보려고 한다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

![logo](/assets/img/basic99.png)

## Heap - 힙 자료구조
---
  우선 순위 큐는 힙(heap) 자료구조를 기반으로 만들어져 있기 때문에, 힙(heap) 자료구조에 대해서 간단하게 짚고 넘어가자면 다음과 같다.

-  완전 이진 트리 구조 : 힙은 완전 이진 트리(Complete Binary Tree) 구조를 가진다. 완전 이진 트리란 마지막 레벨을 제외한 모든 레벨이 노드로 꽉 채워져 있고, 마지막 레벨의 노드는 왼쪽부터 채워지는 트리 구조를 말한다.

힙 속성 : 힙은 주로 다음과 같은 두 가지 속성을 가진다.

- 최대 힙(Max Heap) : 부모 노드가 자식 노드보다 크거나 같은 값을 가진다. 따라서 루트 노드가 가장 큰 값을 가진다.
-  최소 힙(Min Heap) : 부모 노드가 자식 노드보다 작거나 같은 값을 가진다. 따라서 루트 노드가 가장 작은 값을 가진다.

주요 기능으로는 다음과 같이 삽입, 삭제, 정렬이 있는데, 원소를 추가하고 삭제할시 정렬을 통해서 완전 이진 트리구조를 유지하게 된다.

 **삽입(insert)**: 새로운 원소를 힙에 추가합니다. 일반적으로 힙의 마지막 위치에 원소를 추가한 후, 원소를 힙 속성에 맞게 재정렬(Heapify up)한다.

**삭제(delete)**: 힙에서 특정 원소를 삭제합니다. 일반적으로 루트 노드를 삭제하고, 힙의 마지막 원소를 루트로 이동한 후에 재정렬(Heapify down)한다.

**힙 정렬(heapify)**: 힙 속성을 유지하도록 원소들을 재배치하는 과정이다. 삽입이나 삭제 후에 수행된다.
>선택 정렬을 개선한 알고리즘으로, O(n log n)의 시간 복잡도를 가진다. 정렬되지 않은 배열을 최대 힙으로 만든 후 루트를 추출하면서 정렬한다.

힙은 데이터를 추가하고 삭제하는 연산에 O(log n)의 시간 복잡도를 가지며, 특히 우선순위 큐와 관련된 문제를 효율적으로 해결하는 데 널리 사용된다.

## PriorityQueue - 우선 순위 큐
---
Java에서 제공하는 Queue 인터페이스의 구현체 중 하나인 PriorityQueue는 우선 순위 큐를 구현한  것으로, 우선순위가 높은 데이터에 먼저 접근할 수 있도록 하며, 다익스트라 알고리즘과 같은 그래프 알고리즘에서 최소 비용 경로를 찾는 데 유용하게 사용된다. 

삽입(Insertion) : add(), offer() 메서드를 사용하여 요소를 삽입한다. 삽입 시 최소 힙의 특성을 유지하기 위해 로그 시간(O(log n))이 소요된다. 따라서 삽입 시간 복잡도는 O(log n)이다.

삭제(Removal) : poll() 메서드를 사용하여 최소 요소(루트 노드)를 제거하고 반환한다 큐가 비어있으면 null을 반환한다. 최소 힙의 특성을 유지하기 위해 다시 로그 시간(O(log n))이 소요된다. 따라서 삭제 시간 복잡도 역시 O(log n)이다.

최소 요소 조회(Peek) : peek() 메서드를 사용하여 최소 요소(루트 노드)를 조회한다. 비어있으면 null을 반환하고  O(1) 시간 복잡도를 갖는다.
```java
import java.util.PriorityQueue;

PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.add(5);
minHeap.add(3);
minHeap.add(7);
System.out.println(minHeap.peek()); // 출력: 3 (가장 작은 값)
System.out.println(minHeap.poll()); // 출력: 3 (가장 작은 값 제거)
```

우선 순위 큐는 Queue 인터페이스에서 보았던 삽입 삭제 조회 메서드 말고도 추가적으로 다음과 같은 메서드도 제공해준다.

remove(Object o) : 큐에서 특정 요소 o를 제거한다. 요소가 삭제되면 true를 반환하고, 요소가 큐에 없으면 false를 반환한다.
```java
boolean removed = pq.remove(5);
```
isEmpty() : 큐가 비어 있는지 여부를 반환한다. 큐가 비어 있으면 true, 아니면 false를 반환한다.
```java
boolean empty = pq.isEmpty();
```
size() : 큐에 포함된 요소의 개수를 반환한다.
```java
int size = pq.size();
```
clear() : 큐의 모든 요소를 제거하여 비운다.
```java
int size = pq.size();
```
toArray() : 큐의 모든 요소를 배열로 반환한다.
```java
Object[] elements = pq.toArray();
```
iterator() : 큐의 요소를 반복적으로 접근하기 위한 반복자(iterator)를 반환한다.
```java
Iterator<Integer> iterator = pq.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```
### Reference
---
