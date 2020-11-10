---
layout: post
title:  "웹서버의 구성"
categories: [Class, Spring]
---

## 웹서버의 구성
### Client
- 서버에 자료를 요청하는 프로그램(브라우저, Application 등등)

### WebServer
- 요청을 받고, 요청에 대한 응답을 빠르게 만들고 Client에 보낸다.

### Servlet & JSP
- 동적인 자료를 생성해 내는 것. HTML, JSON 형태 등으로 응답한다. (Tomcat, WAS등등)
- 이전에는 Web Server에서 정적인 페이지를, Servlet에서 동적인 페이지를 담당했지만 최근 페이지의 구성이 많아지고 트래픽이 증가하면서 Load Balancer에 의해 처리할 서버가 결정된다.

### Load Balancer
  - 서비스에서 발생하는 트래픽의 양이 많을 때, 하나의 서버가 이를 담당하지 않고 여러 대의 서버가 분산하여 담당해서 서버의 과부하, 속도저하등을 개선하는 서비스이다.
  - 서버 할당 방식
    - Round Robin: 지정된 시간동안 서버를 할당하고, 지정된 시간 후에는 Ready Queue로 보내서 다시 순서를 기다린다. 할당되는 것이 자주 교환된다면, Overhaed가 자주 발생해 비효율적일 수 있다.
    - Least Connection: 연결 개수가 가장 적은 서버를 선택하는 방식이다. 트래픽으로 인해 세션이 길어지는 경우 권장하는 방식이다.
    - Source: 사용자의 IP를 Hashing하여 분배하는 방식이다. 사용자는 항상 같은 서버로 연결되는 것을 보장한다.
	- Balancer의 고장에 대비하여 여분의 Balancer를 마련하고, Main이 망가지면 여분의 Balancer를 활용한다.

### Web Container
  - Servlet, JSP를 실행할 수 있는 소프트웨이다
  - Tomcat, Eclipse Jetty등이 있다.

### WAS
- Web Server와 Web Container가 합쳐진 것이다.
- 사용자의 요청에 따라 동적인 프로그램을 실행하고, 그 결과를 정적인 페이지로 반환한다.
- 직접 동작을 수행하지 않고, 어떠한 Servlet을 통해 응답을 처리할 것인지 결정한다.
- 동작 과정
  1. 웹서버를 통해 필요한 페이지를 요청한다.
  2. Web Container가 Web.xml을 참조해 쓰레드를 생성하고 HttpServletRequest, HttpServletResponse를 생성해 쓰레드로 전달한다.
  3. Web Container는 요청에 맞는 `doGet`, `doPost()` 등의 Servlet 메소드를 호출한다.
  4. 메소드를 통해 생성된 동적 페이지는 HttpServletResponse 객체에 저장되어 WebContainer에 전달된다.
  5. WebContainer는 HttpServletResponse객체를 HttpResponse 객체로 전환하여 웹서버에 전달하고 쓰레드를 종료, 객체를 소멸시킨다.