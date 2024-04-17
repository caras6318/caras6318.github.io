---
title: Spring MVC(4) HTTP 요청 방법
date: 2024-04-12 21:04 +0900
categories: Spring
tags:
  - JAVA
  - Spring
---
## Intro
---
HTTP 요청 메시지를 통해 클라이언트에서 서버로 데이터를 전달하는 방법을 알아보았다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

### **GET**  쿼리 파라미터
---
/url**?username=hello&age=20**  
메시지 바디 없이, URL의 쿼리 파라미터에 데이터를 포함해서 전달한다.
ex) 검색, 필터, 페이징등에서 많이 사용하는 방식

>`request.getParameter()` 는 하나의 파라미터 이름에 대해서 단 하나의 값만 있을 때 사용해야 한다.
>중복일 때는 `request.getParameterValues()` 를 사용해야 한다.
### **POST**  HTML Form  
---
메시지 바디에 쿼리 파리미터 형식으로 전달 username=hello&age=20 
> HTML Form을 사용하면 Content-Type 이 x-www-form-urlencoded 가 된다.

ex) 회원 가입, 상품 주문, HTML Form 사용
![[HttpMessageBody.png]]

클라이언트(웹 브라우저) 입장에서는 두 방식에 차이가 있지만, 서버 입장에서는 둘의 형식이 동일하므로, `request.getParameter()` 로 편리하게 구분없이 조회할 수 있다.
### **HTTP message body**  데이터를 직접 담아서 요청 
---
>HTTP API에서 주로 사용, JSON, XML, TEXT

데이터 형식은 주로 JSON 사용 
서버간 통신 이나 JS를 사용해서 요청할 때 주로 사용된다.
POST, PUT, PATCH

#### JSON
---
**JSON**은 **J**ava**S**cript **O**bject **N**otation 의 약자이다.

직역하면 '자바 스크립트 객체 표기법'으로 데이터를 쉽게  **교환** 하고 **저장** 하기 위한 텍스트 기반의 데이터 교환 표준이다.

JSON은 **텍스트 기반**이기 때문에 다양한 프로그래밍 언어에서 데이터를 읽고 사용할 수 있다.

JSON의 기본적인 형태는 아래와 같다. 

```
{ key : value }
```

JSON의 형태는 **키(Key)** 와  **값(value)** 의 쌍으로 이루어져 있는 구조다.

그리고 Key와 Value사이에는 **콜론(:)** 이 들어간다.

```
{key1 : value, key2 : value2}
```

여러 데이터를 나열할 경우 **쉼표( , )** 를 사용한다.

```
{ key1 : { inKey : inValue }, key2 : [arr1, arr2 arr3] }
```

```
{"판매자정보" : { "이름" : "남도일", "지역" : "서울" } , "판매품목" : ['사과','배','딸기']  }
```

**객체(Object)** 는 **중괄호( { } )** 로 묶어서 표현하고, **배열(Array)** 은 **대괄호( [ ] )** 로 묶어서 표현한다.

>JSON 결과를 파싱해서 사용할 수 있는 자바 객체로 변환하려면 Jackson, Gson 같은 JSON 변환 라이브러리 를 추가해서 사용해야 한다. 스프링 부트로 Spring MVC를 선택하면 기본으로 Jackson 라이브러리 ( `ObjectMapper` )를 함께 제공한다.
### Reference
---
