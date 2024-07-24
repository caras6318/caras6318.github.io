---
title: 99클럽 코테 스터디 3일차 TIL Comparator
date: 2024-07-24 15:07 +0900
categories: JAVA
tags:
  - 99클럽
  - 코딩테스트준비
  - 개발자취업
  - 항해99
  - TIL
  - CodingTest
---
![basic99](assets/img/basic99.png)

## Intro
---
코딩테스트를 준비하면서 최근 지원직무에 맞는 언어를 요구하는 기업들이 늘어남을 느끼고 기존에 사용하던 파이썬 에서 자바로 언어를 변경해서 코딩테스트를 준비해야 할 것 같아 항해99에서 진행하는 코테스터디 에 참여하기로 해 보았다. 오늘로 3일차를 맞이하는데 오늘 문제는 프로그래머스 12915번 문제를 풀면서 알게 된 내용에 대해서 작성해 보려고 한다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

### 문자열 배열 정렬
---
자바에서 주로 사용하는 문자열 배열의 정렬 방법은 다음과 같다.

1. Arrays.sort() 메서드 -> 문자열 배열을 오름차순으로 정렬
2. Comparator 인터페이스 사용 -> 이번 풀이에 사용한 방법, 정렬기준을 정할 수 있다.
3. Collections.sort() 메서드 (리스트 정렬) -> 문자열을 리스트에 담아서 정렬하고 싶을 때 사용
4. 람다 표현식을 사용한 정렬 -> 함수형 인터페이스 구현에 사용 간결하고 코드 가독성이 높다.

이번 문제는 주어진 인덱스 번호에 있는 알파벳을 기준으로 정렬을 하고 동일할 경우 해당 문자열로 비교를 해야 하기 때문에 정렬 기준을 정할 수 있는 Comparator를 사용하기로 했다.

### Comparator
---
Comparator 인터페이스는 단 하나의 추상 메서드 compare()를 가지고 있다.

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

두 개의 객체를 인자로 받아 비교한 후 결과를 반환하는 메서드로 일반적으로 결과에 따라 정수를 반환하고, 반환값이 0보다 작으면 첫 번째 인자가 작음을 의미하고, 0이면 같음, 0보다 크면 첫 번째 인자가 크다는걸 의미한다.

이를 응용하여 다음과 같은 코드를 작성했다.

```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String[] solution(String[] strings, int n) {
        
        Comparator<String> CharComparator = new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                // 두 문자열의 n 번째 문자를 비교
                char c1 = s1.charAt(n);
                char c2 = s2.charAt(n);
                
                if (c1 == c2) {
                    // 두 번째 문자가 동일한 경우에는 문자열 전체를 비교하여 정렬
                    return s1.compareTo(s2);
                } else {
                    return Character.compare(c1, c2);
                }
            }
        };

        Arrays.sort(strings, CharComparator);
        return strings;
    }
}
```

이 코드를 람다식으로 작성하면 다음과 같다.

```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String[] solution(String[] strings, int n) {
        // 람다 표현식으로 Comparator 정의
        Comparator<String> CharComparator = (s1, s2) -> {
            char c1 = s1.charAt(n);
            char c2 = s2.charAt(n);

            if (c1 == c2) {
                return s1.compareTo(s2);
            } else {
                return Character.compare(c1, c2);
            }
        };

        Arrays.sort(strings, CharComparator);
        return strings;
    }
}
```
### Reference
---
[문제 바로가기](https://school.programmers.co.kr/learn/courses/30/lessons/12915)