---
layout: post
title:  "Garbage Collection"
categories: [Class, Java_Basic]
---
## Garbage Collection
### 정의
- JAVA 프로세스가 동작하는 과정에서 Heap 영역에 존재하는 더 이상 필요하지 않은 객체를 메모리에서 제거하여 프로그램의 메모리를 효율적으로 사용하게 해준다.
- JVM에서 스케줄링을 통해 개발자가 메모리관리를 직접적으로 해야 할 부담을 줄여준다.

### GC를 도입하게 된 가정
- 대부분의 객체는 금방 접근이 불가능한 상태가 된다.
- 오래된 객체에서 새로운 객체로의 참조는 매우 드물게 일어난다.

### Heap 메모리의 구성
- Young
  - Eden:
    - 처음 생성된 객체가 저장되는 공간이다. bump-the-point 기술을 통해 메모리에 빠르게 저장된다.
      - bump-the-point: 메모리 영역의 마지막 객체를 추적하면서(마지막 객체는 영역의 가장 위), 새로운 객체가 메모리 영역에 적합하면 가장 위에 새로운 객체를 위치하게된다.
    - 이 공간에서 더 이상 호출되지 않는 객체는 Minor GC가 발생하면 사라지게 된다.
    - 사라지지 않은 객체들은 객체가 들어있는 Survivor로 넘어간다.
    - 영역이 가득찬 경우 GC가 발생한다.
  - Survivor(2개):
    - 해당 영역은 Survivor1, Survivor2로 구성되어 있으며 Minor GC가 발생할 떄 참조되지 않는 객체를 제거한다.
    - 남은 객체는 다른 Survivor로 보낸다. 이 과정을 통해 하나의 Survivor는 무조건 비어있는 상태를 유지한다.
    - 각 객체는 Survivor 영역에서 Survivor 영역으로 이동할 때 고유의 Age bit가 1씩 증가하게 된다.
- Old
  - Survivor영역에 있는 객체 중, Age bit가 MaxTenuringThreshold라는 설정값을 초과한 객체가 넘어오게된다.
  - Old 영역에 있는 객체들은 영역이 가득찬 경우 GC를 진행하는데, 5가지 방법의 GC가 있다.
  - Old 영역에서 GC가 일어날 때는, Stop-The-World(STO)가 발생하며 이때는 GC를 제외한 모든 쓰레드가 중단된다.

### Old 영역의 GC
- Serial GC
  - 이전의 CPU가 1개이던 시절 사용하던 방식이다.
  - 하나의 쓰레드로 GC를 진행하고, mark-sweep-compact 과정을 진행한다.
    - mark: 참조가 되지 않는 삭제해야할 객체를 선택한다.
    - sweep: 선택된 객체를 삭제한다.
    - compact: 삭제되지 않은 객체를 연속되게 합치고, 힙의 앞부분에 위치시켜서 객체가 있는 부분과 없는 부분으로 영역을 분할한다.
  - GC가 진행되는 동안 STO가 발생하기 때문에 오래걸리는 Serial GC는 지양하는 것이 좋다.
- Parallel GC
  - Serial GC와 동작 과정은 비슷하지만, 여러개의 쓰레드를 통해 작업을 진행한다.
  - 속도가 더 빠르기 때문에 메모리가 충분하고 코어의 개수가 많을 때 사용하면 좋다.
  - GC 속도를 빠르게하여 STO 기간을 줄인다.
- Parallel Old GC
- CMS GC
- G1 GC

참고: https://d2.naver.com/helloworld/1329,      https://mirinae312.github.io/develop/2018/06/04/jvm_gc.html