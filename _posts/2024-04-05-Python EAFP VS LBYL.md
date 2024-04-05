---
title: Python EAFP VS LBYL
date: 2024-04-05 04:04 +0900
categories: Python
tags:
  - Python
---

## Intro : EAFP - 허락보다 용서구하는 것이 쉽다.
---
파이썬은 EAFP 스타일을 권장하지만 이 내용을 찾아보게 된 이유는 코딩테스트를 준비하면서 백준에서 문제를 풀다 다른 분의 조언을 보았기 때문이다.
> 아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

## EAFP VS LBYL 

EAFP, LBYL 은 코딩 철학의 일종으로 각각 다음과 같은 뜻을 가지고 있다.

EAFP(**E**asier to **A**sk **F**orgiveness than **P**ermission) 의 줄임말. 허락보다 용서구하는 것이 쉽다.
> EAFP 스타일은 코드는 예외가 발생할 수 있는 부분을 시도한 다음에 예외를 처리한다. try-except 사용

LBYL(**L**ook **B**efore **Y**ou **L**eap)의 줄임말. 뛰기전에 봐라. 라는 뜻.
>LBYL 스타일은 작업을 수행하기 전에 먼저 조건을 검사합니다. 이것은 if 문을 사용하여 구현

LBYL 코딩 스타일
```python
if key in dic:
    process(dic[key])
else:
    process(None)

# As an expression:
process(dic[key] if key in dic else None)
```

EAFP 코딩 스타일
```python
try:
    process(dic[key])
except KeyError:
    process(None)

# As an expression:
process(dic[key] except KeyError: None)
```

나는 보통 Main 에서는 EAFP로 작성하고 함수를 작성할때는 LBYL로 작성하고 있었는데 작성양식을 이런 축약어로 정리해서 부른다는 점도 처음알았고 각각 장단점이 있다는 것을 이번 공부를 통해서 알게 되었다.

또한 이 내용은 다음에 `sys.stdin.readline()` 와 `input()` 의 작성방법에 대해서 공부하다가 찾아보게 된 내용이어서 다음에는 두 메서드에 대해서 정리해보려고 한다.
### Reference
---
[파이썬 기본을 갈고 닦자](https://wikidocs.net/16062)
[suwoni-colab](https://suwoni-codelab.com/python%20기본/2018/03/06/Python-Basic-EAFP/)
[PEP-0463](https://www.python.org/dev/peps/pep-0463/)
