---
layout: post
title:  "Thread Pool"
categories: [Class, Java_Basic]
---
## Thread Pool
### 특징
- Thread를 계속 만들어서 사용할 경우, Thread는 작업을 마치고 종료된다.
  - Thread를 생성/삭제하는 오버헤드가 계속 발생한다.
- Thread를 미리 생성하고, 작업을 Thread에 할당하여 동작한다면 오버헤드를 줄일 수 있다.
- 이때 미리 생성해둔 Thread의 집합을 **Thread Pool** 이라고한다.
- 대용량 작업이나, 순서를 제어할 필요가 없는 작업에 주로 사용한다.
- `corePoolSize()`: 오랫동안 작업을 하지 않아도 제거하지 않는 Thread의 수
- `maximumPoolsize()`: 생성할 수 있는 Thread의 최대 수
- `new SynchronousQueue<Runnable>()`: 작업을 queue에 저장하고, queue에 있는 작업을 Thread에 할당한다.


### 순서
1. Thread Pool 생성
2. Thread에 할당할 작업 생성
3. Thread에 작업 요청
4. Thread Pool 종료

### Thread Pool 생성
- newCachedThreadPool 사용
  - 요청 작업보다 Thread가 부족하면 새 Thread를 생성한다.
  - 60초동안 일하지 않은 Thread는 제거한다.(시간은 설정 가능하다.)
    - 이 과정을 통해 Thread의 수를 안정적으로 제어한다.
  - 기본 설정 값으로 Thread의 수는 `Integer.MAX_VALUE`, 시간은 60초이다.
  - `ExecutorService pool1 = Executors.newCachedThreadPool();`

- newFixedThreadPool 사용
  - Thread의 수를 고정시킨다.
  - 현재 Thread의 수보다 작업의 수가 더 많다면, 작업은 Queue에 저장되고 작업이 끝난 Thread가 Queue에서 하나를 할당받는다.
  - 진행중인 작업중, 실패하는 작업은 대기중이던 다른 작업으로 대체한다.
  - 오랫동안 작업이 진행되지 않는 Thread도 제거하지 않는다.
  - `ExecutorService pool2 = Executors.newFixedThreadPool(10);`

- 직접 Thread Pool 구현
  - new ThreadPoolExecutor(corePoolSize, maximumPoolSize, keepAliceTime, TimeUnit, RunnableQueue) 로 구현할 수 있다.
  - 예를 들면 다음과 같이 선언한다.
```java
ExecutorService es = new ThreadPoolExecutor(
     	10, // 코어 스레드 개수
    	100, // 최대 스레드 개수
    	120, // 대기 시간
    	TimeUnit.SECONDS,
    	new SynchronousQueue<Runnable>()
);
```

### Thread에 할당할 작업 생성
- Runnable, Callable interface를 implements 해서 만들 수 있다.
- Runnable은 return값을 줄 수 없다.
```java
class Work implements Runnable{
      @Override
      public void run() {
          for (int i = 0; i < 100; i++) {
               System.out.println(i);
          }
      }
}
```

- Callable은 return값을 줄 수 있다.
```java
class CallableWork implements Callable<String>{
      @Override
      public String call(){
          return "작업 종료";
      }
}
```

### Thread에 작업 요청
- `execute()`: 작업 처리 중 에러가 발생한다면, 해당 Thread를 제거하고 새로운 Thread를 생성해서 작업을 처리한다.
- `submit()`: 작업 처리 중 에러가 발생해도 Thread를 재사용한다.
- `pool1.execute(new Work());` `pool1.submit(new Work());`로 요청할 수 있다.
- Callable로 선언한 객체의 return값을 받을 때는 future 객체를 사용한다.
- `future = pool1.submit(new CallableWork());`로 요청할 수 있다.

### Future 객체
- Callable 작업의 return 값을 받을 수 있는 객체이다.
- 내장된 메소드로 Thread의 흐름을 제어할 수도 있다.
- `get()`: Callable 작업이 끝날때까지 Blocking한다.
- `cancel(true/false)`
  - true인 경우 Interrupt Exception을 발생시켜서 실행중인 객체를 중단시킨다.
  - false인 경우 Interrupt Exception을 발생시키지 않는다.
  - true와 false 모두 get()을 통해 결과값을 받을 수 없다.(CancellationException 발생)

### Thread Pool 종료
- 작업을 모두 실행해도 자동으로 종료가 되지 않기 때문에 직접 종료해야한다.
- `pool.shutdown()`: `Thread.join()`과 마찬가지로 Thread가 종료될때까지 기다렸다가 Thread Pool을 종료한다. Non Blocking이다.

[Github Link](https://github.com/chundh/java-til/blob/master/5_JavaAdvanced/src/com/company/day9/ThreadPool/ThreadPool.java)