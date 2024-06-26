---
title: Spring MVC(5) MVC패턴
date: 2024-04-15 22:04 +0900
categories: Spring
tags:
  - JAVA
  - Spring
---
## Intro
---
이번 포스팅에서는 서블릿, 템플릿엔진(JSP), MVC패턴에 대해서 정리해 보았다. 
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

## Servlet & 템플릿 엔진
---
서블릿을 사용하면 정적인 HTML과는 다르게 회원목록, 도서검색결과 와 같이 동적으로 원하는 HTML페이지를 만들수 있지만 복잡하고 비효율 적이다. HTML문서에서 동적으로 변경해야 하는 부분만 자바코드를 넣어서 사용할 수 있다면 보다 편리해지기에 템플릿 엔진(JSP, Thymeleaf)이 개발되게 된다.

## JSP
---
jsp 파일은 다음과 같은 JSP문서임을 뜻하는 명령어를 첫줄에 작성해야한다.
```java
<%@ page contentType="text/html;charset=UTF-8" language="java" %>`
```

해당 명령어를 제외하고는 HTML파일과 동일한데, 서버 내부에서 서블릿으로 변환되기 때문이다.
JSP는 `<% %>` 다음과 같은 태그를 사용해서 자바코드를 그대로 이용할 수 있다.

![[BeforeMVC.png]]
## But
---
서블릿은 출력을 위한 View화면을 작성할 때 HTML과 자바코드를 작성하는 작업이 섞여 지저분하고, JSP를 사용했을 때는 View를 위한 HTML작업은 깔끔해지고 동적으로 변경이 필요한 부분만 자바코드를 적용함으로써 불필요한 중복작업을 최소화 할수있다. 

*하지만*

JSP 파일은 비즈니스 로직과 View 영역이 한 파일에 존재하고 거기에 JAVA코드, 데이터를 조회하는 레포지토리 등이 모두 JSP 한 파일에 존재한다. *한 마디로 JSP 가 너무 많은 일을 한다.*
미니 프로젝트에도 JSP파일이 이정도로 복잡한데 큰 프로젝트에서 JSP를 사용하기에는 무리가 있다.

유지보수에 너무 많은 코스트가 들어가기 때문이다.

개발자들은 한 파일이 여러 기능을 담당하는걸 그리 좋아하지는 않는다.
웹 서버와 WAS를 같이 사용하는 것처럼 비즈니스 로직은 서블릿처럼 다른곳에서 처리하고 JSP는 목적에맞게 HTML로 View 화면을 구성하는데 집중하는것이 *MVC 패턴*이라고 한다.

## MVC Pattern
---
하나의 서블릿이나 JSP만 사용해서 비즈니스 로직과 뷰 렌더링까지 전부 하게 되면 너무 많은 역할을 하게되고
유지보수가 어려워진다. HTML을 수정하고 싶어도 JAVA코드하고 섞여있고 JAVA코드를 수정하고 싶어도 
HTML이 엄청나게 많은거다. 심지어 두 작업간의 변경 작업 빈도(*라이프 사이클*)또한 다르다.

MVC : Model View Controller Pattern

MVC 패턴은 위의 문제점을 해결하기 위해서 최적화 되어있는, 어떠한 기능에 특화 되어있는지에 따라  역할을 나눈것을 의미한다.

1. 컨트롤러 : HTTP 요청을 받아서 파라미터를 검증하고 비즈니스 로직을 실행한다. 그후 View에 나타낼 데이터를 Model 객체에 담아서 전달한다.
2. 모델 : 뷰에서 출력할 데이터를 담는 객체이다.
3. 뷰 : 모델에 담겨있는 데이터를 이용해서 HTML생성같이 화면을 구성하는 일만 담당한다. 

![[Aftter MVC.png]]

>Tip. 컨트롤러에 비즈니스 로직을 둘수도 있지만 컨트롤러가 너무 많은 작업을 하게됨으로 Service라는 계층을 둬서 비즈니스 로직만을 처리한다.

![[MVC_P2.png]]

## But 2
---
MVC 패턴을 사용하면 컨트롤러와 뷰의 렌더링 작업을 나누어서 구분할수는 있지만 컨트롤러는 중복되는 코드들이 많다. 같은 View Path를 작성한다던가, View로 이동하는 코드가 항상 중복 호출된다. 반복적인 작업을 메서드로 뽑을수는 있지만 뽑은 메서드를 호출하는것도 중복되는 점이다.

![[BeforeFrontCtrl.png]]

>개발자들은 이렇게 불필요하게 같은 작업을 반복하는걸 싫어한다.
>{: .prompt-info }

그래서 컨트롤러의 공통되는 작업을 없애기 위해서 FrontController 라는걸 두게된다.

![[After FrontCtrl.png]]

### FrontController
---
FrontController의 특징은 클라이언트의 요청을 FrontController서블릿 하나로 처리한뒤
해당 요청에 맞는 컨트롤러를 찾아서 호출한다는 점이다. 이렇게 함으로써 공통적으로 처리해야하는 부분은
FrontController가 담당하기 때문에 다른 컨트롤러들은 서블릿을 사용하지 않아도 된다.

>FrontController == DispatcherServlet
### Reference
---
