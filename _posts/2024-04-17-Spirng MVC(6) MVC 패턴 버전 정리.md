---
title: Spirng MVC(6) MVC 패턴 버전 정리
date: 2024-04-17 23:04 +0900
categories: Spring
tags:
  - JAVA
  - Spring
---
## Intro
---
저번에 정리한 MVC패턴에 이어서 각 버전별로 정리한 내용들입니다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

## FrontController - V1
---
먼저 프론트 컨트롤러을 적용해보면 다음과 같다.

![FC V1](MVC%20V1.png)

프론트 컨트롤러를도입하게 되면 다음과 같은 프로세스를 통해 작업이 처리된다.
1. 클라이언트로부터 요청을 받아 프론트 컨트롤러가 URL매핑정보를 보고 매핑되어있는 컨트롤러를 조회한다.
2. 조회된 컨트롤러를 호출한다.
3. 조회된 컨트롤러는 view(JSP)를 forward한다
4. JSP는 렌더링되어 클라이언트는 HTML응답을 받게된다.


하단의 코드와 같이 서블릿과 비슷한 모양의 컨트롤러 인터페이스를 도입함으로써 각각의 컨트롤러들은 인터페이스를 구현만 하면 된다. 프론트 컨트롤러는 인터페이스를 호출하는 것으로 구현과 관계없이 로직의 일관성을 가져갈 수 있다.

```java
package hello.servlet.web.frontcontroller.v1;

 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.io.IOException;

 public interface ControllerV1 {

     void process(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException;
 }
```

## FrontController - V2
---
인터페이스를 구현해서 컨트롤러를 작성해보면 
```java
package hello.servlet.web.frontcontroller.v1.controller;

 import hello.servlet.domain.member.Member;
 import hello.servlet.domain.member.MemberRepository;
 import hello.servlet.web.frontcontroller.v1.ControllerV1;

 import javax.servlet.RequestDispatcher;
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.io.IOException;

 import java.util.List;
 public class MemberListControllerV1 implements ControllerV1 {

     private MemberRepository memberRepository = MemberRepository.getInstance();

@Override

     public void process(HttpServletRequest request, HttpServletResponse
 response) throws ServletException, IOException {

         List<Member> members = memberRepository.findAll();
         request.setAttribute("members", members);

         String viewPath = "/WEB-INF/views/members.jsp";
         RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);
         dispatcher.forward(request, response);
	}
}
```

이런 형태를 가지게 되는데 

```java
String viewPath = "/WEB-INF/views/new-form.jsp";
RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);
dispatcher.forward(request, response);
```

컨트롤러에서 View단으로 이동하는 부분에 위와 같은 중복된 코드들이 존재하게 된다.
이를 해결하기 위해서 다시한번 공통적으로 뷰를 처리하는 객체를 생성해주는것이 V2다.

![FC V2](MVC%20V2.png)

```java
package hello.servlet.web.frontcontroller;
 import javax.servlet.RequestDispatcher;

 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.io.IOException;

 public class MyView {

     private String viewPath;

     public MyView(String viewPath) {
         this.viewPath = viewPath;

}

     public void render(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException {

         RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);

         dispatcher.forward(request, response);
     }

}

```

위와같은 클래스를 작성해준뒤 상속받아 사용하는 인터페이스를 작성해 준다.

```java
package hello.servlet.web.frontcontroller.v2;
 import hello.servlet.web.frontcontroller.MyView;

 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.io.IOException;

 public interface ControllerV2 {

     MyView process(HttpServletRequest request, HttpServletResponse response)
 throws ServletException, IOException;
 }
```

이렇게 View단만 담당해서 공통적인 부분을 처리해줌으로서 각 컨트롤러는 복잡한 `dispatcher.forward()` 를 직접 생성해서 호출하지 않아도 된다. 단순히 MyView 객 체를 생성하고 거기에 View 이름만 넣고 반환하면 된다.
## FrontController - V3
---
먼저 프론트 컨트롤러을 적용해보면 다음과 같다.

## FrontController - V4
---
먼저 프론트 컨트롤러을 적용해보면 다음과 같다.

## FrontController - V5
---
먼저 프론트 컨트롤러을 적용해보면 다음과 같다.

### Reference
---
