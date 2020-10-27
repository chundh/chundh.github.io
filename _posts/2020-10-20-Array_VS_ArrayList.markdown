---
layout: post
title:  "Array - ArrayList"
categories: [Class, Java_Basic]
---

## 두 배열 형식의 차이
### Array
- 할당된 공간이 정해져 있다.
  * `int[] array = new int[5]`
- 공간을 초과한 인덱스에 접근할 경우 에러를 발생한다.
- Primitive Type(int, long, char)과 Object 데이터를 배열로 사용할 수 있다.
- 마지막 사용한 index에 즉시 접근이 안된다.
  * 초기값이 남아있는 idx가 마지막 idx
- 메모리를 할당하고, 할당된 메모리에서만 데이터를 저장, 호출하므로 속도가 빠르다.

### ArrayList
- 할당된 공간이 변한다.
- 공간을 초과한 인덱스에 접근할 경우 알아서 공간을 확장한다.
  * ArrayList 구현 함수를 보면 `int newCapacity = oldCapacity + (oldCapacity >> 1);`에 해당하는 부분이 있다.
  * 공간이 다 찬 상태에서 추가로 add를 한다면 기존의 공간 크기/2 만큼 배열의 크기를 증가시킨 배열을 생성하고, 기존의 배열을 복사한다.
- Object 데이터만 배열로 사용할 수 있다.
- 마지막 idx를 바로 알 수 있다.
  * `list.size()`를 사용해 list의 크기 파악.
- 배열의 크기를 확장할 경우 복사하는 과정을 거쳐야하므로 속도가 느리다.

### 결론
- 배열의 크기가 정해진 데이터(행렬, 알고리즘 문제에서 제공되는 배열의 범위)를 활용할 때는 Array를 사용하자.
- 배열의 크기가 정해져 있지 않다면 배열의 최대 범위를 생각해보고, ArrayList를 사용한다.
- 만약 배열의 중간에 위치하는 데이터의 삽입, 삭제가 빈번한 경우 LinkedList를 활용하자.