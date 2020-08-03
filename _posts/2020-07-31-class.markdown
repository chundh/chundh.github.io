---
layout: post
title:  "배열, 다차원 배열, 문자열"
categories: Java_Basic
---

### 배열

- 특성
  * 하나의 변수로 여러개의 값을 다룰 수 있다.
  * 동일 자료형만 다룰 수 있다.
  * 한번 선언한 배열의 크기는 변할 수 없다.
  * 배열에 속한 값은 메모리에 연속적으로 존재한다.
- 배열의 선언
```
	int[] integers;
	integers = new int[10];
	int[] arr = new int[10];
	int[] integers2 = new int[]{0,2,3,4,5,2,3,6}; //배열의 크기를 지정하지 않고 생성할 수 있다.

	-> int로 선언시에 각 인덱스의 값은 0으로 초기화된다.
	-> 배열 사용시에 선언해준 범위 밖의 인덱스로 접근하면 에러 발생!
```
- 배열과 반복문의 활용
```
	for(int i=0; i<floats.length; i++){
        System.out.println(floats[i]);
    }

    //Enhanced for 아니면 for each 구문이라 부름
    for(float floatval: floats){
        System.out.println(floatval);
    }
    -> 위 두개 코드는 같은 역할을 한다.
```

### 다차원 배열(N-D Arrays)

- 특성
  * 배열이 배열을 담고 있으면 다차원 배열이라 한다.
- 다차원 배열의 선언
```
	int[][] arr = new int[10][5];
    int[][] arr1 = new int[10][];
    for(int i=0; i<arr1.length; i++){
        arr1[i] = new int[5];
    }
    int[][] arr2 = new int[5][];
    arr2[0] = new int[1];
    arr2[1] = new int[5];
    arr2[2] = new int[2]; => 다차원 배열의 하위차원의 크기는 서로 다를 수 있다.
```

### 문자열

- 특성
  * 문자들은 내부적으로 '클래스'로 구성되어있다.
  * 내부에는 문자의 배열로 된 데이터가 있다.(char [])
  * 한번 만든 문자열은 변하지 않는다.
  * 문자열 편집은 String을 쓰지 않고 Builder나 Buffer를 사용한다.
- 문자열의 생성
```
	String s1 = "문자열 생성 방법"; // 문자열을 곧바로 생성할 경우 상수 풀에서 찾아서 사용
	String s2 = new String("문자열 생성 방법"); // 문자열을 클래스로 생성할 경우 새로운 값을 생성

	System.out.println(s1 == s2); // false
    메모리 참조 값이 다르기 때문에 밑의 방식으로 해야 정상적으로 String값 계산을 할 수 있다.
    System.out.println(s1.equals(s2)); // true

    s1.indexOf("a") // 해당 문자의 index값 return
    s1.equalsIgnoreCase("AadB"); // 대소문자를 구분하지 않고 계산
    s1.replace("l", "t"); // 기존의 string을 바꾸는 것이 아니라, string을 새로 생성해서 출력
    s1.substring(0,s1.length()); // 0~s1의 길이-1 까지의 문자열을 출력
    s1.trim(); // 문자열의 공백을 제거한 문자열을 출력
```