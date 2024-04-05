---
title: Python Join()
date: 2024-04-05 07:04 +0900
categories: Python
tags:
  - Python
  - CodingTest
---
## Intro
---
코딩테스트 문제를 풀다보면 딕셔너리나 리스트에 들어있는 문자열들을 출력하는 경우가 종종 있는데
자주 사용하다보니 한번 정리해 두는게 좋을것 같아 공부해 보았다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

## str.join()
---
먼저 공식 문서를 찾아보면 다음과 같이 나온다.

Return a string which is the concatenation of the strings in _iterable_
>  _iterable_ 객체 내부의 문자열들을 연결해서 문자열을 반환한다고 한다.

_iterable_ 이란 반복 가능한 객체를 뜻하며
대표적으로 iterable한 타입으로는  list, dict, set, str, bytes, tuple, range등이 있다.
  
join() 메서드가 왜 필요하냐는 질문에 대한 대답으로는 아래의 코드를 보면 이해하기 쉽다.

```python
a = ['a', 'b', 'c', 'd', '1', '2', '3']

print(a) # ['a', 'b', 'c', 'd', '1', '2', '3']
print()

# 리스트를 문자열로 : join 이용

result1 = "".join(a)

print(result1) #abcd1234

# 리스트를 문자열로 : 반복문을 통해 하나하나 문자열을 더하기.

result2 = ''
for v in a:
    result2 += v
   
print(result2) # abcd1234
```

for문을 사용해서 출력할수도 있지만, 내장함수를 이용해서 한번에 출력할 수 있다.
눈치가 빠르다면 이미 알고 있겠지만 str.join()에서 str이 의미하는 바는 *구분자*를 의미한다.

위의 예제에서 "" 를 "@" 로 바꿔준다면 다음과 같다.

```python
a = ['a', 'b', 'c', 'd', '1', '2', '3']

result1 = "".join(a)

print(result1) #abcd1234

result2 = "@".join(a)

print(result2) # a@b@c@d@1@2@3@4

```

리스트의 경우
```python 
# Joining with empty separator
list1 = ['o', 'p', 'e', 'n', 'e', 'r']
print("".join(list1)) # opener

# Joining with string
list1 = " opener "
print("$".join(list1)) # $o$p$e$n$e$r$ 공백도 문자로취급
```

튜플의 경우
```python
# elements in tuples
list1 = ('1', '2', '3', '4')

# put any character to join
s = "-"

# joins elements of list1 by '-'
# and stores in string s
s = s.join(list1)

# join use to join a list of
# strings to a separator s
print(s) # 1-2-3-4
```

set의 경우
```python
list1 = {'1', '2', '3', '4', '4'} 

# put any character to join
s = "-#-"

# joins elements of list1 by '-#-'
# and stores in string s
s = s.join(list1)

# join use to join a list of
# strings to a separator s
print(s) # 1-#-3-#-2-#-4 set의 경우 중복 제거가 이루어진다.
```

딕셔너리의 경우
```python

dic = {'Opener': 1, 'IT': 2, 'Blog': 3}

# Joining special character with dictionary
string = '_'.join(dic)

print(string) # Opener_IT_Blog 딕셔너리의 key값이 문자열일 경우에만 가능

dic = {1: 'Opener', 2:'IT', 3 :'Blog'}
string = '_'.join(dic)

print(string) # ERROR

```

다음과 같이 조건을 줘서도 삽입할 수 있다.
```python
words = ["apple", "", "banana", "cherry", ""]
separator = "@ "
result = separator.join(word for word in words if word)

print(result) # apple@ banana@ cherry
```
### Reference
---
[Python join docs](https://docs.python.org/3/library/stdtypes.html#str.join)
[geek for geeks](https://www.geeksforgeeks.org/python-string-join-method/)