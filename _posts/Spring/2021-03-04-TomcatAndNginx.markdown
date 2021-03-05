---
layout: post
title:  "JSP"
categories: [Class, Spring]
---

## Tomcat
### Tomcat이란?
- 서블릿 컨테이너가 있는 웹 어플리케이션 서버(WAS)이다.
- Tomcat은 웹 서버와 연동하여 실행할 수 있는 자바 환경을 제공한다.
- JSP(Java Servlet Page)와 서블릿이 실행할 수 있는 환경을 제공한다.
- 즉 서버를 열고, 클라이언트의 요청에 응답할 수 있게끔 도와준다.
- Spring Boot에는 Tomcat이 내장되어서 알아서 웹서버에 Java프로그램을 띄워준다.

## Nginx
- 사용자가 WAS에 직접 접근하거나, 많은 사용자가 갑자기 하나의 WAS에 몰리는 경우 보안, 속도면에서 문제가 생길 수 있다.
- 이때 **무언가**가 WAS앞에서 이를 로드밸런싱해주고, WAS는 사용자에게 노출이 되지 않는 상태라면 보안, 속도면에서 많이 개선이 될 것이다.
- 이를 위한 그 **무언가**의 역할을 Nginx가 할 수 있다.

### Nginx란?
- Nginx는 보안과 속도면에서 Apache보다 많이 개선된 Web Server이다.
- 하나의 웹서버에 10000개의 클라이언트 접속을 동시에 다루기 위해 Event Driven구조의 http, Reverse Proxy를 제공한다.
- 클라이언트의 요청을 받고, 적절한 WAS로 클라이언트의 요청을 넘겨준다.

## Tomcat과 Nginx의 연동
- 이 둘을 연동하면 웹 서버를 구성할 때 성능의 향상을 기대할 수 있다.
- 정적인 페이지는 Nginx가 바로 응답하고, 동적인 페이지의 경우 WAS에 요청을 넘겨서 처리할 수있다.

### 연동 과정
- nginx.conf 파일을 설정해줘야한다.
  - http 블록 안에 `upstream`을 설정한다.
  ```
  upstream api1{
      server localhost:8080;
  }
  upsream api2 {
      server localhost:8081;
  }
  ```
  - `server` 블록 안에 `location` 블록을 생성하고 그 안에 `proxy_pass`를 설정한다.
  ```
  location /api1{
      proxy_pass http://api1;
  }
  location /api2{
      proxy_pass httpL//api2;
  }
  ```
- hosts에 내가 사용할 도메인과 ip, port를 넣어줘야한다.
  - vi /etc/hosts
  ```
  127.0.0.1 8080 api1;
  127.0.0.1 8081 api2;
  ```
- 이후 Nginx와 Tomcat을 실행해주면 80포트로 접속을 해도 8080포트로 접속이 되는걸 볼 수 있다.