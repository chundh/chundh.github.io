---
layout: post
title:  "Http Connection"
categories: [Class, Computer_Science]
---

## Http 연결 방식
### Short-lived Connection
- Http 1.0에서 기본으로 사용되던 방식이다.
- TCP 3Hand Shake 과정을 거쳐서 연결을 이루고 나면, 하나의 요청에 대한 응답을 받고 연결을 닫는다.
- 지속적으로 요청이 있는 경우에 3Hand Shake 과정을 반복해서 연결을 해야하므로 비효율적이다.

![short-lived connections](https://user-images.githubusercontent.com/42088125/98533178-fb014c00-22c5-11eb-81a9-60bbcb70d676.JPG)

### Persistent Connection
- Http 1.1버전에서 추가된 방식이다.
- 요청에 대한 처리를 한 후 일정 시간동안 요청을 기다리고, 응답한다.
- 3Hand Shake 과정이 줄어들기 때문에, TCP의 성능을 향상시킬 수 있다.
- 다수의 사용자가 요청하는 경우에 한 사용자가 connection을 점유하여 비효율적일 수 있다.
  - 이를 방지하기 위해 `KeepAliveTimeout`와 `MaxKeepAliveRequests`을 설정한다.
  - `KeepAliveTimeout`: 요청을 기다리는 시간이다. 기본 설정값은 15초이다.
  - `MaxKeepAliveRequests`: 한번의 연결동안 처리할 요청의 수이다. 기본 설정값은 100회이다.

![persistent connections](https://user-images.githubusercontent.com/42088125/98533238-0c4a5880-22c6-11eb-9d32-8b6d20552ecc.JPG)

### Http Pipelining
- Http 1.1버전에서 추가된 방식이다.
- 기본적으로 Http의 요청은 순차적이다. 하나의 요청에 대한 응답을 받고 다음 요청을 하는 방식으로 이루어져있다.
- 같은 `Persistent connection`을 사용해 요청에 대한 응답을 받기전에 추가적인 요청을 해서, 응답 지연률을 줄인다.
- 버그가 있는 프록시들이 많고, 구현이 어렵다.

![http pipelining](https://user-images.githubusercontent.com/42088125/98533282-1b310b00-22c6-11eb-965d-24dc63a49917.JPG)

참고 : https://developer.mozilla.org/ko/docs/Web/HTTP/Connection_management_in_HTTP_1.x