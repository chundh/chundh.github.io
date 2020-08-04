---
layout: post
title:  "자바 기초용어, 변수"
categories: Java_Basic
---

### 용어정리
- JVM(Java Virtual Machine) : 바이트 코드로 빌드된 것이 동작이 이루어지게끔 필요한 환경에 알맞게 도와주는 것.
- IDE(Integrated Development Environment) : 통합 개발 환경. 프로젝트 관리, 빌드 등의 다양한 기능을 제공하여 개발을 수월하게하도록 도와준다.
- SSH를 생성하면 .ssh 폴더에 id_rsa 와 id_rsa.pub가 생성된다. id_rsa.pub 파일은 public 키로서 사용이 되고, id_rsa는 private 키로서 다른사람에게 절대 노출이 되면 안되는 키이다.



###변수
- 변수명 설정시 주의해야 할 것
    * 자바에서 이미 사용되는 키워드는 사용할 수 없다.(ex. int, char 등)
    * 숫자, 한글로 시작할 수 있지만 왠만하면 사용하지 말자.
    * 특수문자를 사용할 수 없다.($ 제외)

- 변수명은 어떻게 설정해야 할까?
    * 소문자로 시작하는 것이 주로 쓰이는 방법
    * 숫자로 사용해야 할 때가 있다면 "_8" 같이 언더바를 사용하도록 한다.
    * 변하지 않는 수는 전부 대문자로 쓰고 띄어쓰기는 언더바로 사용한다.(ex. STATIC_VARIABLE)
    * 두개의 단어 이상을 합쳐서 사용할 때는 각 첫 단어의 대문자를 사용한다. 이를 camelCase라고 한다. (ex. lowerCamelCase)
    * 클래스, 인터페이스 등의 이름은 대문자로 시작하고 연결되는 첫 단어도 대문자를 사용한다. 이를 PascalCase라고 한다.(ex. ClassFirst)

- 변수의 선언
```
int x; // 변수 선언
x = 10;  // 10은 리터럴이라고 부른다.
//리터럴:어딘가에 저장되어있지 않은 순수한 값.
```

- DataTypes
    * 자료형 - 기본형(Primitive Type), 참조형(Reference Type)
    * 기본형 - 정수형, 실수형, 문자형, 논리형
    * 참조형 - 문자열(String)
    * 메모리의 효율성을 생각하여 데이터 크기에 맞는 데이터 타입을 사용해야 한다. 이때 데이터 타입의 크기보다 큰 데이터를 넣게 된다면 Overflow가 발생하게 된다.
    * 정수형
```
//BYTE : 1byte로 구성
        System.out.println(Byte.MAX_VALUE); // 0을 표현하기 위해 2^7 -1
        System.out.println(Byte.MIN_VALUE); // -2^7
        //BYTE의 데이터 범위는 -128~127

        //SHORT : 2byte로 구성
        System.out.println(Short.MAX_VALUE); // 2^15-1
        System.out.println(Short.MIN_VALUE); // -2^15
        //SHORT의 데이터 범위는 -32768~32767

        //INTEGER : 4byte로 구성
        System.out.println(Integer.MAX_VALUE); // 2^31-1
        System.out.println(Integer.MIN_VALUE); // -2^31
        //INTEGER의 데이터 범위는 -2147483648~2147483647

        //Long : 8byte로 구성
        System.out.println(Long.MAX_VALUE); // 2^63-1
        System.out.println(Long.MIN_VALUE); // -2^63
        //Long의 데이터 범위는 -9223372036854775808~9223372036854775807
        
        //숫자 리터럴의 기본형은 int이다.
        short shortA = 10;
        short shortB = 20;
        //short shortC = shortA + shortB; => short타입 두개를 더하면 short데이터타입의 크기가 넘어갈 수 있으므로 강제로 형변환을 해줘야 한다.
        short shortC = (short)(shortA + shortB);

        int bigInt = Integer.MAX_VALUE;
        int biggerInt = bigInt+1; // Overflow가 발생한다.

        //long veryBigInt = 10000000000; => int보다 큰 값을 넣을경우 에러가 발생한다. 이때 마지막에 L을 붙여준다.
        long veryBigInt = 10000000000L;
```
    * 진수법
```
Binary(2), Octal(8), Decimal(10), Hexadecimal(16)
        System.out.println(0b1101); // 2진수
        System.out.println(071); // 8진수
        System.out.println(1424); // 10진수
        System.out.println(0x11); // 16진수
```
