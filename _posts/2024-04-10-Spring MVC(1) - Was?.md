---
title: Spring MVC(1)
date: 2024-04-10 20:04 +0900
categories: Spring
tags:
  - JAVA
  - Spring
---
## Intro
---
Spring MVC 강의를 듣고 정리하 내용입니다.
>아래 내용은 공부한 내용을 정리한 것으로 틀린 내용이 포함되어 있을 수 있습니다.  

### 웹 서버(Web Server)
---
HTTP 기반으로 HTML, CSS, JS 와 같은 정적 데이터들을 제공하는 것 ex) NGINX, APACHE

### 웹 어플리케이션 서버(WAS - Web Application Server)
---
HTTP 기반으로 동작하며 웹 서버 기능 포함하기 때문에 정적 리소스 제공도 가능 하며, 프로그램 코드를 실행해서 애플리케이션 로직 수행한다.  ex) 톰캣(Tomcat) Jetty, Undertow
- 동적 HTML, HTTP API(JSON)
- 서블릿, JSP, 스프링 MVC

### 차이점
---
*웹 서버는 정적 리소스(파일), WAS는 애플리케이션 로직* 하지만, 사실은 둘의 용어도 경계도 모호하다.

>웹 서버도 프로그램을 실행하는 기능을 포함하기도 함
웹 애플리케이션 서버도 웹 서버의 기능을 제공함 

자바는 서블릿 컨테이너 기능을 제공하면 WAS 
서블릿 없이 자바코드를 실행하는 서버 프레임워크도 있음
WAS는 애플리케이션 코드를 실행하는데 더 특화

### 웹 시스템 구성 WAS, DB
---
WAS 와 DB 만으로도 웹 시스템을 구성할 수는 있다.

![[was+db 1.png]]

하지만 was가 너무 많은 작업을 담당하게 되고, 서버 과부화가 우려된다.
정적 리소스 때문에 어플리케이션 로직이 처리가 안될 수 있다 -> 오류 화면도 노출 안됨

![[wasERR.png]]

이런 문제점을 해결하기 위해서 구성에 WEB 서버를 추가한다.

![[was+web.png]]

가벼운 정적 리소스는 웹 서버가 처리하게 하고 어플리케이션 로직같은 동적인 처리는 WAS에 넘긴다.
더 많이 사용되는 리소스에 맞춰서 효율적으로 리소스 관리가 가능하다.

![[wasERR+web.png]]

WAS 와 DB으로만 구성할 때와는 다르게 WAS에 문제가 생겨도 오류화면을 노출할 수 있다.
### Reference
---
[스프링 MVC](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)
