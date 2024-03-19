---
title: Algorithm 기초
date: 2024-03-19 21:03 +0900
categories: Algorithm
tags:
  - Python
  - CodingTest
---

저번에 작성하던 Github Page를 사용해서 블로그를 작성하는건 내용을 정리해서 마저 작성하는걸로 하고 이번에는 코딩테스트를 대비하면서 알고리즘과 자료구조등을 다시한번 정리해 보려고 한다.

## 1. 문자열

---
### 1.1 자주 사용하는 자료형
---
1. 리스트 
	리스트는 여러 개의 데이터를 연속적으로 담아 처리하기 위해 사용할 수 있다. JAVA 에서의 Array(배열)같은 기능을 포함하고 있으며, 내부적으로 LinkedList 자료구조를 채택하고 있어서 append(), remove() 등의 메서더를 지원한다. Python의 리스트는 C++ 의 STL vector와 비슷해 배열 혹은 테이블이라고 부르기도 한다.
	
	대괄호([]) 안에 원소를 넣어서 초기화 하며, 쉼표로 원소를 구분한다.
	리스트의 원소에 접근할 때는 인덱스값(0부터 시작하는)을 괄호 안에 넣는다. 비어있는 리스트를 선언하고 싶을 때는 list() 또는 [] 를 이용해서 선언할 수 있다.

```python
	a = [1, 2, 3, 4, 5]
	
	print(a)
	>>> [1,2,3,4,5]
	#두번째 원소에 접근
	print(a[1])
	>>> 2
	#빈 리스트 선언
	
	a = list()
	print(a)
	>>> []
	
	a = []
	print(a)
	>>> []
	
	# 크기가 N이고, 모든 값이 0인 1차원 리스트 초기화
	n = 10
	a = [0] * n
	print(a)
	>>> [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

1. **리스트 인덱싱 / 슬라이싱**

	```python
	a = 'abcd efg'
	
	print(a[0], a[1], a[2], a[-2], a[-1]) 
	>>> a b c f g
	
	print(a[1:5]) 
	>>> bcd
	
	print(a[-3:-1]) 
	>>> ef
	
	print(a[:]) 
	>>> abcd efg
	
	print(a[3:]) 
	>>> d efg
	
	print(a[:3]) 
	>>> abc
	```

2. **특정 문자가 있는지 확인**

```python
	a = 'abcde'
	
	print('d' in a) 
	>>> True
```

3. **문자열이 같은지 비교**

```python
	a = 'hello'
	b = 'hello'
	
	print(a is b) 
	>>> True
```

4. **문자열 길이 반환**

```python
	a = 'hello'
	
	print(len(a)) 
	>>> 5
```

5. **특정 문자의 인덱스 값 찾기**

```python
	a = 'hello'
	
	print(a.index('h')) 
	>>> 0
```

6. **문자열을 구분자 기준으로 나누고 합치기**

```python
	a = 'h,e,l,l,o'
	
	print(a.split(',')) 
	>>> ['h', 'e', 'l', 'l', 'o']
```

7. **문자열 대소문자 변환**

```python
	a = 'a,b,c,D,E'
	
	print(a.upper()) 
	>>> A,B,C,D,E
	
	print(a.lower()) 
	>>> a,b,c,d,e
```

8. **기존 값을 다른 값으로 치환**

```python
	a = 'h,e,l,l,o'
	
	print(a.replace(',', '/')) 
	>>> h/e/l/l/o
```

9. **양쪽 끝에서 특정 문자(혹은 공백) 제거**

```python
	a = '   abc   '
	print(a.strip()) 
	>>> 'abc'
	
	a = '12321abc111'
	print(a.strip('123')) 
	>>> abc
```

10. **아스키코드로 변환 혹은 대소 비교**

```python
	print(ord('a') > ord('b')) 
	>>> False
	
	print(ord('a') , ord('b')) 
	>>> 97 98
```

11. **리스트 컴프리헨션**
	리스트를 초기화 하는 방법중의 하나로 대괄호 안에 조건문과 반복문을 넣어서 리스트를 초기화할 수 있다. 
	
	```python
	array = [i for i in range(20) if i % 2 == 1]
	
	print(array)
	>>> [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

	이런 방법을 응용하면 2차원 리스트를 초기화 할때 효과적으로 사용할 수 있다.
	```python
	n = 3
	m = 4
	array = [[0] * m for _ in range(n)]
	
	print(array)
	>>> [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]
```

	
	
	


### 내일 공부할 내용들

1. **GCD/LCM** (최대공약수, 최소공배수)
 
2. **소수 판별** (에라토스테네스의 체와 제곱근을 이용한 소수 판별법)

3. **나머지, 몫 구하기** 

4. **순열, 조합**(내장 라이브러리 사용안하고 구현해보기)

> 추가로 알아두면 좋은 개념
> 
> - 진법 변환(2진수, 8진수, 16진수 등)
> - 소인수분해


### Reference
---
