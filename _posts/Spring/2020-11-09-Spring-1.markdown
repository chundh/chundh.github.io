---
layout: post
title:  "HTTP"
categories: [Class, Spring]
---

## HTTP
- HyperText Transfer Protocol
- Connectionless
  - TCP의 특성을 통해 연결한 후 한번 연결하고나서 연결을 끊는다.
    - Ex. 네이버를 한번 접속하고나서, 인터넷을 끊어도 현재 페이지가 변하지 않는다.
- Stateless
  - 요청을 하면 요청에 맞는 응답만 준다.
  - 하지만 자신의 상태를 변화시켜야 하는 경우에 이를 반영하지 못한다는 단점이 있다.
    - Ex. 장바구니에 무언가를 담았는데, 새로고침하니 반영되지 않는 경우 -> 이것을 쿠키로 해결할 수 있다.

### TCP/UDP
- IP끼리 통신할 때 사용하는 방식
- TCP
  - 한쪽에서 자료를 요청하면, 상대측에서 응답을 한다(ACK, NACK).
  - 상대방이 자료를 보내고 정상적으로 받았는지 확인한다.
  - 위의 `3Hand Shake` 과정으로 신뢰성이 있다.
- UDP
  - 요청에 대한 응답이 아닌, 일방적으로 자료를 보낸다.
  - 신뢰성이 없는 통신 타입이다.
    - `parity check`를 통해 어느정도의 에러를 수정할 수 있다. 하지만 너무 많은 에러의 경우는 복구가 되지 않는다.
  - 속도가 빠르다.

### 요청 메세지(Request Message)
- Method를 결정한다.(GET, POST)
  - GET: 정적인 페이지 하나를 요청하는 것이며 한정된 데이터만을 전송할 수 있다.
    - ex. GET /member/insert.jsp?name=천도희&age=27
    - url에 정보가 포함이 되어서 보안에 취약하다.
  - POST: GET과 비슷하게 동작하지만, 내부에 존재하는 body에 image, text등을 포함하여 추가적인 요청을 할 수 있다.
- 요청 헤더 정보
  - Mozila, Chrome, Safari 등의 페이지가 보여지는 것을 포함해서 서버상에서 어떠한 페이지를 넘겨줄지 결정할 때 사용한다.
- CRUD 알아보기

### 응답 메세지(Response Message)
- 응답 코드(200, 404, 503 등등)
- 응답 헤더
  - Retry After: 503에러와 함께 쓰이며, 일정 시간이 지난 후 문서요청을 하라는 의미
  - Location: 300응답일 때, 어느 주소로 이동할지를 명시한다. 빈칸이면 새로고침하라는 의미이다.
- 메세지 바디에 해당응답 내용을 포함한다.(ex. www.naver.com을 구성하는 html이 해당. f12)

### 캐시
- 매번 같은 요청에대한 응답을 할 때, 새로 응답을 만들어야 하나에 대한 질의에서 나온 개념
- 이를 활용해서 고쳐야 할 부분(매번 바뀌는 광고, 실시간 검색어 등등)과 고치지 않아도 되는 부분(HTML 구성이 캐시에 저장되어있다.)을 구분한다.
- 캐시를 활용해 업데이트 주기, 응답 횟수 등을 정할 수 있다.

참고: https://jeong-pro.tistory.com/80

### web.xml
- web에 관련된 전체 사전 설정을 하는 곳.

### Context
- 어플리케이션 하나의 시작부터 끝가지의 흐름
- URI에서 포트번호 뒤에 것들이 하나의 Context이다.

### Add configuration
- Tomcat 연결할 때 밑에 `Warning: No artifacts marked for deployment`와 함께 Fix가 뜬다.
- 이때 Fix를 exploded로 바꿔주고 context를 바꿀 수 있다.

### gradle
- 환경별로 사용해야 할 설정이 다를 때, 간단한 프로그래밍을 통해 이를 설정할 수 있다.

### servlet
- Tomcat은 servlet을 동작시키는 기능을 담당한다.
- JAVA 객체이다.
- 웹 컨테이너 내부에서 동작하는 컴포넌트로서 동적인 부분을 담당한다.
- 멀티 쓰레드 모델로 동작한다.
- 요청이들어오면 하나의 스레드가 생성되고, 요청을 처리한 후 종료되는 형식이다.
- 이러한 과정을 서블렛으로 만들면 톰캣이 이를 제어한다.

- 목적
  - 자바 서블릿 API를 지원하는 서버의 기능을 점진적으로 확장
  - 서블릿으로 구현되면 프로세스 대신에 쓰레드를 생성하기 때문에 속도가 빠르다.
    - 기존의 CGI 방식에서는 프로그램이 실행될 때마다 프로세스가 생성이 되서, 속도가 느렸다.
- 서블릿은 동적인 것을 생성하는 과정을 조절할 뿐, 무거운 기능을 직접 수행하지 않는다.(MVC모델에서는 Controller역할)



- Http Servlet
- Http ServletRequest: 클라이언트에서 요청한 req message가 담긴다.
- Http ServletResponse: 웹서버에서 클라이언트로 넘기는 res message가 담긴다. servlet이 종료가 되면 response가 클라이언트로 넘어간다. Heap영역에 존재하면서 setter를 통해서 response에 메세지가 저장된다.

- doGet(), doPost() 등의 메소드를 오버라이드 해놓으면 tomcat에서 이들을 알아서 호출한다.

- Servlet Mapping을 통해서 기본 도메인을 저장하고, 그 이후 쿼리문에 대해 어떠한 서블릿을 실행할지를 결정한다.
- `<servlet-name>config</servlet-name>`
- `<url-pattern>/servletConfig.do</url-pattern>`
- 톰캣에서 req메세지를 Servlet Message로 변환하고, 이를 doGet, doPost 메소드에서 Servlet Response에 내용을 채워넣은 다음, 메소드가 종료되면 톰캣이 ServletResponse를 페이지orJSON형태로 변환하여 웹서버로 보내준다.