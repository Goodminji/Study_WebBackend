# ThreadLocal

쓰레드란 ? 한 프로세스 내에서 동작 되는 여러 실행 흐름 



ThreadLocal 이란?

* ThreadLocal class 는 오직 한 쓰레드에 의해서 읽고 쓰여질 수 있는 **변수**
* 두 쓰레드가 같은 코드를 실행하고 이 코드가 하나의ThreadLocal 변수를 참조 하더라도 서로의 ThreadLocal 변수를 볼 수 없다.
* ThreadLocal 변수를 선언하면 멀티쓰레드 환경에서 각 스레드마다 독립적인 변수를 가지고 접근 할 수 있다.
* ThreadLocal은 한 쓰레드에서 실행되는 코드가 동일한 객체를 사용할 수 있도록 해주기 때문에 관련된 코드에서 파라미터를 사용하지 않고 객체를 각자가 가져다 쓸때 사용 된다.
  * 사용자 인증 정보 Spring Security 에서 사용자마다 다른 인정 정보를 사용할때 & Session정보
  * 출처 :[https://yeonbot.github.io/java/ThreadLocal/](https://yeonbot.github.io/java/ThreadLocal/)

