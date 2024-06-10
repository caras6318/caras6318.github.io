---
title: Spring Junit
date: 2024-04-22 20:04 +0900
categories: 
tags:
---
## Intro
---
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

## JUnit5

---

> **💡 JUnit5**  
> **- Java 언어에서 독립된 단위 테스트(Unit Test)를 지원해 주는 프레임워크를 의미합니다.**  
> - JUnit 5의 경우 'Java8 이상 버전'부터 지원을 하며 JUnit Platform, Jupiter, Vintage 모듈이 결합된 형태를 가지고 있습니다.

![](https://blog.kakaocdn.net/dn/b9dqSW/btsBykPG0kx/10WOvh5va061KXBnwdvXF1/img.png)

> **💡 단위 테스트(Unit Test)**  
>   
> - 소프트웨어 개발에서 개별적인 코드 단위를 테스트하는 것을 의미합니다.  
> - 코드의 작은 부분을 격리시켜 독립적으로 테스트함으로써 코드의 정확성과 신뢰성을 검증합니다.  
> - 자동화가 되고 반복 가능하며 버그를 빠르게 찾아내고 수정하는데 도움이 됩니다. 또한 코드 변경 시 기존 기능에 영향을 주지 않고 코드의 동작을 확인하는 데 유용합니다.  
> **💡 단위 테스트의 범위**  
> - 클래스, 메소드, 함수와 같은 작은 단위의 코드를 격리시켜 독립적으로 테스트하는 것을 의미합니다.  
> - 따라서, 컨트롤러단이나 서비스단과 같은 구성 요소는 각각 개별적인 단위로 테스트될 수 있습니다.

   
   
   
 

## JUnit5 구성요소

---

>  **💡 jUnit5 구성요소**  
>   
> **- JUnit5에서는 Platform, TestEngine Interface, TestEngine, Jupiter, Vintage으로 구성이 되어 있습니다.**

![](https://blog.kakaocdn.net/dn/9aMoo/btsBBowOeZ2/gBTDXWmEDxS2elxxGKv9o1/img.png)

https://www.swtestacademy.com/junit-5-architecture/

|   |   |
|---|---|
|**구성 요소**|**설명**|
|**JUnit Platform**|- JUnit 테스트를 실행하는데 사용되는 실행환경입니다.   <br>- 이는 다양한 TestEngine 구현체를 실행하고 테스트 결과를 보고하는 역할을 수행합니다.|
|**TestEngine Interface**|- JUnit Platform에서 테스트 엔진을 정의하는 데 사용됩니다.   <br>- 이 인터페이스를 구현하여 사용자 정의 테스트 엔진을 만들 수 있습니다.|
|**TestEngine**|- JUnit Platform에서 테스트를 실행하는 데 사용되는 구현체입니다.   <br>- 각각의 TestEngine은 특정한 테스트 프레임워크 또는 런처와 통합되어 동작하며, 테스트 수명주기 관리, 테스트 실행, 결과 보고 등의 기능을 제공합니다.|
|**JUnit Jupiter**|- JUnit 5에서 제공되는 새로운 프레임워크입니다.   <br>- 이는 테스트 작성과 실행을 위한 새로운 기능과 어노테이션을 제공하며, JUnit 4보다 더 강력하고 유연한 테스트 코드 작성이 가능합니다.|
|**JUnit Vintage**|- JUnit 4와의 하위 호환성을 제공하기 위한 모듈입니다.   <br>- 이 모듈은 JUnit 4로 작성된 테스트를 JUnit 5 플랫폼에서 실행할 수 있게 해줍니다.|

   
   
   
 

### 1. JUnit Platform
---

> **💡 JUnit Platform**  
>   
> **- JUnit 테스트를 실행하는 데 사용되는 실행 환경을 의미합니다. TestEngine Interface를 통하여 다른 TestEngine 구현체들과 상호작용하여 테스트를 실행하고 테스트 결과를 보고하는 역할을 수행하는 테스트 프레임워크입니다.**  
> - 테스트의 수행 과정은 발견, 실행, 결과 보고의 과정을 통해서 수행이 됩니다.

   
 

> **💡 JUnit Platform의 주요 특징**  
> **1. JUnit Platform에서 TestEngine Interface를 통해 테스트 엔진(Jupiter, Vintage)과 상호작용을 합니다.**  
> - 테스트 엔진과의 통신을 통해 테스트 수명주기 관리, 동적 테스트 검색 및 실행, 테스트 결과 보고 등을 지원합니다.  
>   
> **2. JUnit 3, 4, 5와 같은 테스트 프레임워크를 지원합니다.**   
> - JUnit 5와의 호환성을 제공하며, JUnit 4로 작성된 테스트를 JUnit 5 플랫폼에서도 실행할 수 있도록 하는 모듈을 포함하고 있습니다.  
>   
> **3. 다양한 환경 및 설정에서 테스트를 실행할 수 있습니다.**   
> - 테스트 실행을 위한 표준화된 인터페이스를 제공하여 다양한 테스트 프레임워크와 런처가 통합될 수 있도록 합니다. 이를 통해 개발자는 자신이 선호하는 테스트 프레임워크를 사용하여 테스트를 작성하고, JUnit Platform에서 실행할 수 있습니다.

   
 

> **[ 더 알아보기 ]**  
> **💡Test Framework와 TestEngine의 차이는?**  
>   
> - 테스트 프레임워크는 테스트를 작성하고 실행하기 위한 구조와 규칙을 제공하며 TestEngine은 테스트를 실행하는 엔진으로 테스트를 ‘실제 실행하고 결과를 반환하는 역할’을 담당합니다.

   
   
 

### 2. TestEngine Interface

---

> **💡 TestEngine Interface**  
> **- JUnit Platform에서 테스트를 실행하고 결과를 보고하는 데 사용이 되는 인터페이스로 TestEngine에 대한 메서드와 속성을 정의하는 데 사용이 됩니다.**  
> - TestEngine Interface를 기반으로 TestEngine의 구현체를 구성합니다. 이를 통해 사용자 정의 TestEngine을 만들 수 있습니다.

> **💡 [참고]** TestEngine Interface의 주요 메서드

|   |   |   |
|---|---|---|
|**메서드**|**리턴 타입**|**설명**|
|**discover()**|void|- 테스트를 발견하고 고유한 ID를 부여하는 메서드입니다.|
|**execute()**|void|- 테스트를 실행하는 메서드입니다.|
|**getId()**|String|- 테스트 엔진의 고유 식별자를 반환하는 메서드입니다.|
|**getGroupId()**|String|- 테스트 엔진의 그룹 식별자를 반환하는 메서드입니다.|
|**getVersion()**|String|- 테스트 엔진의 버전을 반환하는 메서드입니다.|

   
   
 

### 3. TestEngine

---

> **💡 TestEngine**  
> **- TestEngine Interface의 구현체로 테스트를 실행하는 데 사용이 됩니다.**  
>   
> - 각각 TestEngine은 특정한 테스트 프레임워크 또는 런처와 통합되어 동작하며, 테스트 수명주기 관리, 테스트 실행, 결과 보고 등의 기능을 제공합니다.

   
   
   
 

### 4. JUnit Jupiter

---

> **💡 JUnit Jupiter**  
>   
> **- JUnit 5에서 제공되는 새로운 프레임워크를 의미하며 테스트 작성과 실행을 위한 기능을 어노테이션을 제공하며 JUnit4 보다 강력하고 유연한 테스트 코드를 작성하도록 제공해 줍니다.**

   
 

> **💡 [참고]** JUnit Jupiter의 주요 어노테이션  
>   
> - 3) 주요 어노테이션 & 메서드 부분에서 상세하게 알아봅니다.

|   |   |
|---|---|
|**어노테이션**|**설명**|
|**@Test**|테스트 메서드를 정의하는 데 사용되는 어노테이션입니다. 이 어노테이션이 지정된 메서드는 JUnit Jupiter에서 테스트로 실행됩니다.|
|**@ParameterizedTest**|매개변수화된 테스트를 정의하는 데 사용되는 어노테이션입니다. 이 어노테이션이 지정된 메서드는 여러 매개변수를 사용하여 반복적으로 실행됩니다.|
|**@BeforeEach**|각각의 테스트 메서드가 실행되기 전에 실행되는 코드를 정의하는 데 사용되는 어노테이션입니다.|
|**@AfterEach**|각각의 테스트 메서드가 실행된 후에 실행되는 코드를 정의하는 데 사용되는 어노테이션입니다.|

   
   
 

### 5. JUnit Vintage

---

> **💡 JUnit Vintage**  
> **- JUnit 3, 4의 TestEngine을 JUnit 5 플랫폼에서 사용할 수 있도록 제공을 합니다.**  
> - JUnit 5 플랫폼을 사용하여 JUnit 4 테스트를 실행할 수 있으며, JUnit 5의 다양한 기능과 호환성을 유지할 수 있습니다. 또한 기존의 테스트 코드를 유지하면서도 JUnit 5의 새로운 기능과 개선점을 활용할 수 있습니다.

   
   
 

### 6. 구성 요소 별 전반적인 흐름

---

> **💡 구성 요소 별 전반적인 흐름**  
>   
> 1. 사용자는 IDE Tool을 이용하여 테스트 코드를 실행합니다.  
>   
> 2. 테스트 코드는 JUnit Platform 내에서 수행이 됩니다.  
>   
> 3. 테스트 코드를 구성하는 메서드나 어노테이션에 대해서는 TestEngine Interface를 이용하여 호출하여 구성합니다.  
>   
> 4. TestEngine Interface의 실제 구현되는 구현체는 Junit Jupiter, Junit Vintage, Custom Engine을 기반으로 구현이 됩니다.

![](https://blog.kakaocdn.net/dn/bBQVxx/btsBvfVLPHS/0B6TBWuT4YD7H9kGMHSiKk/img.png)

   
   
   
   
 

## 3) JUnit 5 주요 어노테이션 & 메서드
---

### 1. JUnit 5 어노테이션
---

>  **💡JUnit 5 어노테이션****- JUnit Jupiter에서는 테스트 구성 및 프레임워크 확장을 위해 다음 어노테이션들을 지원합니다.**

|   |   |
|---|---|
|**어노테이션**|**설명**|
|**@Test**|테스트 메소드임을 나타내는 어노테이션|
|**@ParameterizedTest**|매개변수화된 테스트를 위한 어노테이션|
|**@RepeatedTest**|반복적으로 실행되는 테스트를 위한 어노테이션|
|**@TestFactory**|동적으로 테스트를 생성하는 팩토리 메소드를 정의하는 어노테이션|
|**@TestTemplate**|테스트 템플릿을 정의하는 어노테이션|
|**@TestClassOrder**|테스트 클래스의 실행 순서를 지정하는 어노테이션|
|**@TestMethodOrder**|테스트 메소드의 실행 순서를 지정하는 어노테이션|
|**@TestInstance**|테스트 인스턴스의 생명주기를 지정하는 어노테이션|
|**@DisplayName**|테스트의 표시 이름을 설정하는 어노테이션|
|**@DisplayNameGeneration**|테스트의 표시 이름을 동적으로 생성하는 어노테이션|
|**@BeforeEach**|각 테스트 메소드 실행 전에 실행되는 메소드를 정의하는 어노테이션|
|**@AfterEach**|각 테스트 메소드 실행 후에 실행되는 메소드를 정의하는 어노테이션|
|**@BeforeAll**|모든 테스트 메소드 실행 전에 실행되는 메소드를 정의하는 어노테이션|
|**@AfterAll**|모든 테스트 메소드 실행 후에 실행되는 메소드를 정의하는 어노테이션|
|**@Nested**|중첩된 테스트 클래스를 정의하는 어노테이션|
|**@Tag**|테스트를 그룹화하기 위한 태그를 지정하는 어노테이션|
|**@Disabled**|비활성화된 테스트를 나타내는 어노테이션|
|**@Timeout**|테스트의 제한 시간을 설정하는 어노테이션|
|**@ExtendWith**|커스텀 확장을 적용하는 어노테이션|
|**@RegisterExtension**|커스텀 확장을 등록하는 어노테이션|
|**@TempDir**|테스트용 임시 디렉터리를 생성하는 어노테이션|
    
### 2. JUnit 5 Assertions 메서드
---

> **💡 JUnit Assertions**  
> **- 단위 테스트에서 다양한 유형의 검사를 수행하기 위한 일련의 Assertions 메서드를 제공합니다. 이러한 어서션은 테스트되는 코드의 예상 동작을 확인하는 데 도움이 됩니다.**  
>   
> - 모두 import org.junit.jupiter.api.Assertions 패키지를 임포트 하여서 사용합니다.

|   |   |   |
|---|---|---|
|**메서드**|**구분**|**설명**|
|**assertEquals**(expected, actual)|JUnit 4~|예상값과 실제값이 동일한지 확인합니다.|
|**assertArrayEquals**(expected, actual)|JUnit 4~|예상 배열과 실제 배열이 동일한지 확인합니다.|
|**assertNull**(object)|JUnit 4~|객체가 null인지 확인합니다.|
|**assertNotNull**(object)|JUnit 4~|객체가 null이 아닌지 확인합니다.|
|**assertSame**(expected, actual)|JUnit 4~|예상값과 실제값이 같은 객체인지 확인합니다.|
|**assertNotSame**(expected, actual)|JUnit 4~|예상값과 실제값이 다른 객체인지 확인합니다.|
|**assertTrue**(condition)|JUnit 4~|조건이 참인지 확인합니다.|
|**assertFalse**(condition)|JUnit 4~|조건이 거짓인지 확인합니다.|
|**assertAll**((Executable... executables)|JUnit 5|모든 단언문(assertion)이 성공하는지 확인합니다.|
|**assertIterableEquals**(Iterable<?> expected, Iterable<?> actual)|JUnit 5|예상 가능한 순서로 반복 가능한 항목이 동일한지 확인합니다.|
|**assertLinesMatch**((List<String> expectedLines, List<String> actualLines)|JUnit 5|두 문자열 목록이 일치하는지 확인합니다.|
|**assertNotEquals**(Object unexpected, Object actual)|JUnit 5|예상값과 실제값이 동일하지 않은지 확인합니다.|
|**assertThrows**(Class<T> expectedType, Executable executable)|JUnit 5|지정된 예외가 발생하는지 확인합니다.|
|**assertTimeout**(Duration timeout, Executable executable)|JUnit 5|주어진 시간 내에 작업이 완료되는지 확인합니다.|
|**assertTimeoutPreemptively**(Duration timeout, Executable executable)|JUnit 5|주어진 시간 내에 작업이 완료되는지 확인하며, 작업이 중단될 수 있습니다.|


   
   
 

## 4) JUnit 5 활용방안

---

### 1. JUnit 라이프 사이클

---

> **💡 JUnit 라이프 사이클**  
>   
> - JUnit을 구성한 클래스를 구성으로 @Test가 수행되는 기준으로 전후에 수행되는 라이프 사이클에 대해서 알아봅니다.

|   |   |
|---|---|
|**단계**|**설명**|
|**Setup**|각 테스트 메서드가 실행되기 전에 필요한 설정 작업을 수행합니다.|
|**Test**|실제 테스트가 진행되는 주요 단계입니다. 각 테스트 메서드는 개별적으로 실행되며, 코드의 예상 동작을 확인하기 위해 어설션(assertion) 또는 검증(verification)이 수행됩니다.|
|**Cleanup**|각 테스트 메서드가 실행된 후 필요한 정리 작업을 수행합니다.|
|**Suite-level setup and cleanup**|테스트 스위트의 모든 테스트 메서드 실행 전후에 한 번씩 발생합니다. 테스트 스위트 전체에 적용되어야 하는 설정 또는 정리 작업을 수행하는 데 사용됩니다.|

   
 

![](https://blog.kakaocdn.net/dn/MEwrd/btsBx7ixtkF/zSrL8Ee4plLr9DWCud0Ou1/img.png)

> **💡 JUnit 라이프 사이클 수행과정**  
> *** 기본적으로 위에서 아래로 @Test를 선언한 순서에 따라 수행이 됩니다.**  
>   
> **1. [@BeforeAll]** JUnit 클래스가 수행되면 최초 한번 @BeforeAll 어노테이션을 선언한 메서드가 실행이 됩니다.  
>   
> **2. [@BeforeEach]** @Test을 찾았다면 테스트 실행 전 @BeforeEach을 선언한 메서드가 실행됩니다.  
>   
> **3. [@Test]** @Test를 선언한 메서드가 실행됩니다.  
>   
> **4. [@AfterEach]** @Test 실행을 마치면 @AfterEach를 선언한 메서드가 실행됩니다.  
>   
> 5. @Test를 선언한 메서드가 있는지 찾으며 존재하면 (2. 과정)을 반복수행하며, 존재하지 않는 경우 (6. 과정)을 수행합니다.  
>   
> **6. [@AfterAll]** 실행할 @Test가 존재하지 않는다면 @AfterAll을 선언한 메서드를 수행합니다.  
>   
> 7. 테스트를 종료합니다.

   
   
 

### 2. Given-when-then 패턴
---

> **💡 Given-when-then 패턴**  
> **- 테스트 케이스를 더 가독성 있고 유지보수하기 쉽게 구조화하는 방법을 의미합니다.**  
> - 이 패턴을 따르면 테스트 케이스가 더 구체적이고 이해하기 쉬워지며 각각의 단계를 분리하여 각 테스트 부분이 어떤 역할을 담당하는지 명확해집니다.

|   |   |
|---|---|
|**섹션**|**설명**|
|**Given : 설정**|테스트의 초기 상태 또는 사전 조건을 설정합니다. 입력 데이터나 테스트가 실행될 문맥을 지정합니다.|
|**When : 동작**|테스트되는 동작 또는 이벤트를 설명합니다. 테스트되는 특정 메서드나 동작을 나타냅니다.|
|**Then : 검증**|"When" 섹션에서 설명한 동작으로 인해 기대되는 결과 또는 동작을 정의합니다.|

   
 

> **💡 Given-when-then 패턴을 이용한 예시**  
>   
> - Given 섹션에서는 '초기 상태'를 설정하고 When 섹션에서는 '특정 동작을 수행'하며, Then 섹션에서는 '예상 결과를 검증'하는 어서션(assertion)을 사용하여 검증합니다.

```java
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import static org.junit.jupiter.api.Assertions.*;

class MyTest {

    @Test
    void testListSize() {
        // Given
        ArrayList<String> list = new ArrayList<>();

        // When
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");

        // Then
        assertEquals(3, list.size());
        assertTrue(list.contains("Apple"));
        assertFalse(list.isEmpty());
    }
}
```

> **💡 [참고]** 해당 패턴은 BDD의 테스트 시나리오를 작성하는 단계에서도 동일하게 적용이 됩니다.



   
   
   
 

### 3.  JUnit 명명 규칙

---

> **💡 인기 있는 JUnit 명명 규칙**  
>   
> **- JUnit의 메서드명을 지정하는 명명 규칙에 대해 알아봅니다.** **- 이를 통해서 어떤 테스트를 수행하는지 명시적으로 이해할 수 있도록 돕습니다.****- 아래의 글을 참고하여서 작성하였습니다.**

 [7 Popular Strategies: Unit Test Naming Conventions - DZonedzone.com](https://dzone.com/articles/7-popular-unit-test-naming)

   
   
 

#### 2.1. 명명 규칙 -1 : '메서드명_테스트대상상태_예상동작' 형식

> **💡 MethodName_StateUnderTest_ExpectedBehavior**  
>   
> **- '메소드명_테스트대상상태_예상동작' 형식으로 JUnit 메서드 명을 지정하는 방식입니다.**  
>   
> - 이 전략에 대해서는 메소드 이름이 코드 리팩토링의 일부로 변경된다면 이 테스트 이름도 변경되어 나중에 이해하기 어려워진다는 반대 의견이 있습니다.  
>   
>   
> **[ 사용 예시 ]**  
>   
> - isAdult_AgeLessThan18_False : 만약 나이가 18보다 작으면 성인이 아님 (False)을 반환하는 경우  
> - withdrawMoney_InvalidAccount_ExceptionThrown : 잘못된 계정으로 출금 시 예외가 발생하는 경우  
> - admitStudent_MissingMandatoryFields_FailToAdmit: 필수 입력 필드가 누락되었을 때 학생을 입학시키지 못하는 경우

   
   
 

#### 2.2. 명명 규칙 -2 : '메서드명_예상동작_테스트대상상태 '형식

> **💡 MethodName_ExpectedBehavior_StateUnderTest**  
> **- “메서드명_예상동작_테스트대상상태” 형식으로 JUnit 메서드 명을 지정하는 방식입니다.**  
>   
> - 조금 다른 방식으로 변경된 것이지만, 일부 개발자들은 이 명명 기법을 사용하는 것을 권장합니다. 이 기법은 메서드 이름이 변경되면 이해하기 어려워진다는 단점도 있습니다.  
>   
> **[사용 예시]**  
>   
> - isAdult_False_AgeLessThan18: 만약 나이가 18보다 작으면 성인이 아님 (False)을 반환하는 경우  
> - withdrawMoney_ThrowsException_IfAccountIsInvalid: 잘못된 계정으로 출금 시 예외가 발생하는 경우  
> - admitStudent_FailToAdmit_IfMandatoryFieldsAreMissing: 필수 입력 필드가 누락되었을 때 학생을 입학시키지 못하는 경우

   
   
   
 

#### 2.3. 명명 규칙 -3: “test” 접두어 형식

> **💡 test [Feature being tested]**  
>   
> **- “test” 접두어 형식으로 JUnit 메서드 명을 지정하는 방식입니다.**  
> - "test" 접두어가 중복된다는 주장도 있지만, 일부 개발자들은 이 기법을 사용하는 것을 선호합니다. 또한 SonarLint에 code smells를 피할 수 있다는 이유로 권장됩니다.  
>   
> **[사용 예시]**  
>   
> - testIsNotAnAdultIfAgeLessThan18: 만약 나이가 18보다 작으면 성인이 아님을 테스트합니다.  
> - testFailToWithdrawMoneyIfAccountIsInvalid: 잘못된 계정으로 출금 시 실패하는 것을 테스트합니다.  
> - testStudentIsNotAdmittedIfMandatoryFieldsAreMissing: 필수 입력 필드가 누락되었을 때 학생이 입학되지 않는 것을 테스트합니다.

   
   
 

#### 2.4. 명명 규칙-4 : 테스트할 기능 형식

> **💡 Feature to be tested**  
>   
> **- 일부는 메서드를 테스트 메서드로 식별하기 위해 이미 주석을 사용하고 있으므로, 단순히 테스트할 기능을 작성하는 것이 더 좋다고 제안합니다.**  
> - 이는 단위 테스트를 문서의 대체 형태로 만들어주고 SonarLint에 code smells를 피할 수 있다는 이유로 권장됩니다.

   
   
   
 

#### 2.5. 명명 규칙 -5: Should_예상동작_테스트대상상태 형식

> **💡 Should_ExpectedBehavior_When_StateUnderTest**  
>   
> **- 'Should_예상동작_When_테스트대상상태'로 JUnit 메서드 명을 지정하는 방식입니다.**  
>   
> **[사용예시]**  
>   
> - Should_ThrowException_When_AgeLessThan18: 만약 나이가 18보다 작으면 예외를 던져야 합니다.  
> - Should_FailToWithdrawMoney_ForInvalidAccount: 잘못된 계정일 경우 출금에 실패해야 합니다.  
> - Should_FailToAdmit_IfMandatoryFieldsAreMissing: 필수 입력 필드가 누락되었을 때 입학에 실패해야 합니다.

   
   
 

#### 2.6. 명명 규칙 -6: When_테스트대상상태_Expect_예상동작 형식

>  **💡 When_StateUnderTest_Expect_ExpectedBehavior**  
>   
> **- 'When_테스트대상상태_Expect_예상동작'으로 JUnit 메서드 명을 지정하는 방식입니다.**  
>   
> **[사용예시]**  
>   
> - When_AgeLessThan18_Expect_isAdultAsFalse: 만약 나이가 18보다 작으면 성인이 아님 (False)을 예상합니다.  
> - When_InvalidAccount_Expect_WithdrawMoneyToFail: 잘못된 계정으로 출금 시 실패할 것을 예상합니다.  
> - When_MandatoryFieldsAreMissing_Expect_StudentAdmissionToFail: 필수 입력 필드가 누락되었을 때 학생 입학이 실패할 것을 예상합니다.

   
   
 

#### 2.7. 명명 규칙 -7: Given-When-Then 형식

> **💡 Given_Preconditions_When_StateUnderTest_Then_ExpectedBehavior**  
>   
> **- Behavior-Driven Development (BDD)의 일부로 개발된 명명 규칙입니다. 테스트를 사전 조건 (Given), 테스트 대상 상태 (When), 예상 동작 (Then)으로 세 가지 부분으로 나누어 작성합니다.**  
>   
> - 이 접근 방식은 Behavior-Driven Development (BDD)의 일부로 개발된 명명 규칙에 기반을 두고 있습니다. 개별 테스트를 세 부분으로 나눠 사전 조건, 테스트 대상 상태 및 예상 동작을 위의 형식에 맞춰 작성합니다.   
> **[사용예시]**  
> - Given_UserIsAuthenticated_When_InvalidAccountNumberIsUsedToWithdrawMoney_Then_TransactionsWillFail: 사용자가 인증된 상태에서 잘못된 계정 번호를 사용하여 금액을 인출하면 거래가 실패할 것입니다. 

 [7 Popular Strategies: Unit Test Naming Conventions - DZonedzone.com](https://dzone.com/articles/7-popular-unit-test-naming)

  
  
 

> **💡 [참고]** Spring Boot 환경에서 JUnit5를 이용하기 위한 관련 글들입니다.

|   |   |
|---|---|
|**분류**|**URL**|
|**JUnit 5 이론 및 구성 요소**|[https://adjh54.tistory.com/341](https://adjh54.tistory.com/341)|
|**JUnit 5 환경구성 및 활용예제**|[https://adjh54.tistory.com/342](https://adjh54.tistory.com/342)|
|**JUnit 5 + Mockito 이론 및 활용예제**|[https://adjh54.tistory.com/346](https://adjh54.tistory.com/346)|
|**JUnit 5 + MockMvc 이론 및 활용예제**|[https://adjh54.tistory.com/347](https://adjh54.tistory.com/347)|
|**Assertions API Document**|[https://adjh54.tistory.com/348](https://adjh54.tistory.com/348)|

### Reference
---
