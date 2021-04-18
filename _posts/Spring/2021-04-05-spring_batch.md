# 스프링 배치
많은 사용자의 상태 변화를 인지하고 일괄처리해주는 것을 쉽고 안정적으로 지원해주는 것이 스프링 부트 배치이다.

## 장점
- 자동화 : 매번 단순반복작업을 쉽고 빠르게 자동화시켜준다.
- 대용량 처리 : 그것이 대용량이라 할지라도 가장 최적화된 성능을 보장한다.
- 견고성 : 예측하지 못한 상황이나 동작에 대한 예외처리도 정의할 수 있다.
- 재사용성 : 공통적인 작업을 단위별로 재사용할 수 있다.

## 실행 단계
1. 읽기 : 데이터 저장소(보통 데이터베이스)에서 특정 데이터 레코드를 읽는다.
2. 처리 : 원하는 방식으로 데이터를 가공/처리한다.
3. 쓰기 : 수정된 데이터를 다시 데이터베이스에 저장한다.

## 기본 구조

![image](https://media.oss.navercorp.com/user/21775/files/16a3fa80-9ed5-11eb-8a56-6aba30782b56)
- itemReader : 배치데이터를 읽어오는 인터페이스이다. 
- itemProcessor : 읽어온 데이터를 가공/처리한다. 즉, 비즈니스 로직을 처리한다.
- itemWriter : 처리한 데이터를 DB에 저장한다.
- 대용량 데이터에 대한 처리는 일정한 처리 단위로(ex. 100건, 1000건 등) 최대한 단순하게 읽고 처리하고 저장되게 하는 것이 좋다. 그래서 읽고, 처리하고, 저장하는 것으로 단위를 분리한다.
  - chunk라는 단위로 처리되는 수를 정할 수 있다.

## 기본 구조를 포함하는 객체

![image](https://media.oss.navercorp.com/user/21775/files/b4e39080-9ed4-11eb-9ca1-0f29787a4600)
- JobBuilderFactory
  - 생성자에는 JobRepository를 파라미터로 받는다.
  - JobBuilder를 생성하는 JobBuilderFactory에 repository로 설정하여 모든 JobBuilder가 동일한 repository 를 사용하게 된다.
  - get 메소드로 JobBuilder 인스턴스를 생성하여 반환한다.
- JobBuilder
  - JobBuilder를 통해 Job 을 생성할 수 있다.
  - Start, flow 메소드를 통해 step or flow를 파라미터로 받는 Job 인스턴스를 생성한다.
- Job
  - 배치 처리 과정을 하나의 단위로 만들어 표현한 객체이다.
  - Job 객체는 여러 Step 인스턴스를 포함하는 컨테이너이다.
  - JobBuilderFactory 인스턴스를 통해 메소드 체인 형식으로 빌드한다.

```java
@Bean
public Job myJob(JobBuilderFactory jobBuilderFactory) {
    return jobBuilderFactory.get("myJob") // myjob이라는 Job을 생성하는 JobBuilder 인스턴스를 반환받는다.
          .start(mystep) // mystep 메소드를 실행해서 Step 인스턴스를 반환받는다.
          .build(); // myJob이라는 Job이 빌드되면서 Job 인스턴스가 생성된다.
}

@Bean
public Step mystep(StepBuilderFactory stepBuilderFactory) {
    return stepBuilderFactory.get("mystep") // mystep이라는 Step을 생성하는 StepBuilder 인스턴스를 반환받는다.
           .<MemberIn, MemberOut> chunk(100) // 실행 단위를 100건으로 설정한다.
           .reader(myrReader()) // DB에서 원하는 조건의 데이터를 읽어온다.
           .processor(myProcessor()) // 비즈니스 로직을 처리하여 데이터를 처리한다.
           .writer(myWriter()) // 수정된 결과를 DB에 반영한다.
           .build(); // mysetp이라는 Step 인스턴스가 생성된다.
}
```

- JobRepository
  - 배치 처리는 일정한 주기 간격으로 특정 조건에 해당되는 데이터를 읽고, 처리하고, 저장하는 구조이다.
  - 이러한 작업의 처리 정보를 JobRepository 에서 메타데이터의 형태로 저장한다.
  - Job이 실행될 때마다 JobRepository에서는 정보를 담는 JobExcution을 생성한다.
  - 이 JobExcution을 통해 실패한 Job의 인스턴스를 재생성하지 않고, 성공할 때까지 반복해서 실행할 수 있게 된다.


참고
https://ahndy84.tistory.com/18
https://cheese10yun.github.io/spring-batch-basic/