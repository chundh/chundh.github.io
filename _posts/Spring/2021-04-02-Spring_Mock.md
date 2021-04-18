# Mock이란?
- 개발한 기능들을 단위테스트를 하기 위해서 환경을 구축해야할 필요가 있다.
  - 예를 들어, DB에서 데이터 가져오는 것, api호출 등의 기능을 테스트 해야할 때가 있다.
  - 이때 테스트를 할 때마다 매번 DB에 접근한다면 부하가 많이 걸리고, 시간도 많이 걸릴 것이다.
- mock을 이용한다면 이러한 환경을 모두 구성하지 않고 테스트 할 수 있다.
- mock은 테스트 할 때 필요한 실제 객체와 동일한 **모의 객체**를 만들어 테스트의 효율성을 높인다.

## Mock 의 사용
- 테스트할 때 사용되는 클래스의 Mock Object를 만들기 위한 Mock 클래스를 만든다.
- 해당 클래스의 인스턴스를 생성하여 실제 클래스의 인스턴스 대신 테스트에 활용한다.

```java
// mock 클래스
public class ServiceMock {...}

// Test할 때 mock 클래스 활용
public class MockTest {
	@Test
	public void Test() {
    	ServiceMock mock = new ServiceMock();
        ...
    }
}
```

- 각 테스트를 할 때마다 필요한 모든 클래스의 Mock 클래스를 만들게 된다면 이 클래스들을 관리하기 어려워진다.
- 이러한 문제를 Mockito를 사용하여 해결할 수 있다.

## Mockito
- 모든 Mock 클래스를 생성해야했던 문제를 mockito를 사용하여 해결할 수 있다.
- 단위테스트에서 확인할 기능을 제외한 나머지는 중요하지 않다. 그래서 메소드의 실제 내부 동작은 실행되지 않고, 테스트할 상황만 설정해주는 Test Double이라는 개념이 생겼고, Java에서 Test Double을 지원하는 것이 Mockito이다.
- Mockito를 사용하면서 아래의 어노테이션을 자주 접하게된다.
  - @Mock
    - `Mockito.mock()` 코드를 대신할 수 있는 어노테이션이다.
    - 해당 클래스 타입의 Mock Object를 만들어준다.
  - @MockBean
    - SpringBootTest에서 지원하는 어노테이션이다.
    - @Mock 과 비슷하게 동작한다.
    - 스프링 컨텍스트에 mock 객체를 등록하고, @Autowired가 동작할 때 등록된 mock 객체를 주입한다.
  - @Spy
    - 가짜 객체는 실제 메소드를 실행하지 않지만, 경우에 따라 실제 메소드를 실행해야할 때가 있다.
    - 그럴때 @Spy를 사용하여 객체를 stub하게 만든다.
  - @SpyBean
    - Spy와 비슷하다.
  - @InjectMocks
    - 해당 클래스가 필요한 의존성과 맞는 Mock 객체들을 감지하여 해당 클래스의 객체가 만들어질 때 객체를 만들고, 변수에 객체를 주입하게 된다.
    - @MockBean을 사용하는 경우 @InjectMocks로 의존성 주입이 되지 않는다.
    - @InjectMock은 스프링 컨텍스트에 등록된 객체를 찾지 못하고, 클래스 안에서 정의된 mock 객체를 찾아 의존성을 주입하기 때문이다.