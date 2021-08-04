# EventBus

EventBus는 이벤트를 처리할 각 이벤트 리스너를 등록하고 각 리스너에게 이벤트를 전파하는 역할을 수행한다.

1. eventBus pom.xml 등

```text
  <dependency>
      <groupId>com.google.guava</groupId>
      <artifactId>guava</artifactId>
      <version>30.1.1-jre</version>
    </dependency>
```

2. eventBus bean 등

```text
@Configuration
public class EventConfigure {

.....
  // 사용할 Evenbus Bean 등
  @Bean(destroyMethod = "close")
  public JoinEventListener joinEventListener(EventBus eventBus) {
    return new JoinEventListener(eventBus);
  }
}
```

3. 이벤트 리스너 생성 및 등록

이벤트 리스너는 이벤트를 받아 처리하는 객체다. 이벤트를 처리하는 메서드를  구현하고\(JoinEventListener.java\)  **@Subscibe \(com.google.common.eventbus.Subscribe\)** 어노테이션을 달아주면 해당 메서드가 이벤트 핸들러 메서드의 역할을 하게된다.

* 이벤트 객체는 반드시 primitive 타입이 아닌 reference 타입의 객체여야 한다. \(\* reference타입 참조 타입\(reference type\)이란 객체의 번지를 참조하는 타입으로 배열, 열거, 클래스, 인터페이스 타입 

출처: [https://kingpodo.tistory.com/54](https://kingpodo.tistory.com/54) \[킹포도의 코딩\] 

* 핸들러 메서드는 이벤트 객체를 받는 단 하나의 파라미터만 존재해야 한다. 
* 핸들러 메서드의 시그니처는 public void methodName\(Object event\) 형태여야 한다. }

```text
public class JoinEventListener implements AutoCloseable {


  public JoinEventListener(EventBus eventBus) {
    this.eventBus = eventBus;
     // 이벤트 리스너를 이벤트버스에 등록
    eventBus.register(this);
  }
  
  @Subscribe //핸들러 메서
  public void handleJoinEvent(JoinEvent event) {// JoinEvent 필요한 파라미터 담겨져있음.
     ....
  }
}
```

4. 이벤트 발행

* EventBus의 post\(\) 메서드로 이벤트를 발행할 수 있다. 이벤트 버스에 이벤트를 발행하면 해당 이벤트를 구독하고 있는 이벤트 리스너에서 이벤트를 받아 처리하게 된다

```text
@Test
public void postEvent() {
    ...
    eventBus.post(new JoinEvent(evnet));
}
```

{% embed url="https://developer-youngjun.tistory.com/17" %}



