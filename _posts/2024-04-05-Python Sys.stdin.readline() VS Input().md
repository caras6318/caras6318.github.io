---
title: Python Sys.stdin.readline() VS Input()
date: 2024-04-05 07:04 +0900
categories: Python
tags:
  - Python
  - CodingTest
---
## Intro
---
`sys.stdin.readline()` 와 `input()` 메서드는 둘 다 사용자 입력을 받는 데 사용하지만 어떤 차이점이 있는지 알아보자.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

먼저 두 메서드의 공식문서를 찾아보면 아래와 같은 내용들이 나온다.
## input()
---
If the prompt argument is present, it is written to standard output without a trailing newline. The function then reads a line from input, converts it to a string (stripping a trailing newline), and returns that.

>prompt인자가 있을 경우 끝에 개행 문자를 붙이지 않고 표준 출력에 쓴다. 그 후 함수는 입력을 통해 한 줄을 읽고, 문자열로 변환하여 (그 이후 줄 바꿈을 제거) 값을 반환한다.

한마디로 입력 -> 문자열 변환 -> 개행문자 제거 -> 반환 의 프로세스를 거친다.

## sys.readline()
---
The readline module defines a number of functions to facilitate completion and reading/writing of history files from the Python interpreter. This module can be used directly, or via the rlcompleter module, which supports completion of Python identifiers at the interactive prompt. Settings made using this module affect the behaviour of both the interpreter’s interactive prompt and the prompts offered by the built-in input() function.

>readline 모듈은 파이썬 인터프리터에서 completion과 history file의 읽기/쓰기를 용이하게 하는 여러 함수를 정의한다.
이 모듈은 직접 사용하거나, 혹은 interactive prompt에서 파이썬 식별자 완성?(completion of python identifiers)을 지원하는 rlcompleter 모듈을 통해서 사용할 수 있다. 이 모듈을 사용하기 위해서 설정하는 것은 interpreter의 대화식 prompts와 내장 input() 함수가 제공하는 prompt 동작에 영향을 준다.'

---

정리하자면 기능적으로는 비슷하나 실제로는 prompt message을 받을수있는지, 개행문자를 포함하는지가 다르다. `input()` 은 몆가지의 프로세스를 더 거치다보니 시간이 조금더 걸리는편이다. 

따라서 문제가 요구하는데 있어 처리속도가 중요하고 반복문을 통해서 많은 입력이 들어온다고하면 `sys.stdin.readline()`을 사용하는게 바람직하고 아니라면 `input()`을 사용하는게 좋다.

그렇다면 `sys.stdin.readline()`은 저번에 정리한 EAFP 와 LBYL 두 스타일중 어떤 스타일을 따라서 작성해야 할까?

`sys.stdin.readline()`은 파일의 끝(EOF, End of File)을 만나면 빈 문자열을 반환한다. 따라서 일반적으로 `EOFError`를 사용하여 파일의 끝을 감지하는 것은 적합하지 않다. 그렇기에 다음과 같이 LBYL스타일로 작성해 주는게 좋다.

```python
import sys

lines = []

while True:
    line = sys.stdin.readline().strip()
    if line == '':
        break
    lines.append(line)

print("입력된 줄들:")
for line in lines:
    print(line)

```

### Reference
---
[Python Input docs](https://docs.python.org/3/library/functions.html#input)
[Python readline docs](https://docs.python.org/3/library/readline.html)
[점프 투 파이썬](https://wikidocs.net/33#sys)
