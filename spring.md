# Spring

### 1. 어플케이션 컨텍스트 \(application Context\) - 런타임시 모든 빈을 로딩 

* beanFactory\(빈을 사용할때 빈을 로딩 , 빈을 생성하고 관계설정하는 Ioc의 기본기능\) 의 서브 타입으로 오브젝트에 대한 생성과 관계 설정 담당한다.beanFactory의 확정 개\( AOP 기능, 메시지 리소스 핸들링, 이벤트 발생 등 추가기능 제공\)

### 2. 스프링 빈\(bean\)

*   스프링에 의해 IOC 컨테이너 방식\(애플리케이션 컨텍스트\) 으로 관리되는 오브젝트
* IoC\(Inversion of Control, 제어의 역전\)  : 오브젝트 전반에 걸친 모든 제어권을 애플리케이션이 갖는게 아니라 프레임워크의 컨테이너에게 넘기는 개념
* @Configuration \(각 빈을 스프링 애플리케이션 컨텍스트에 제공하는 구성 클래스\) -&gt; @Bean 빈 등록
* @ComponentScan\(자동으로 빈을 등록해주는 어노테이션 \)
* @Component,@Controller,@Configuration,@Repository,@Service 를 빈으로 등록.

### 3. 싱글톤

* 여러 번 빈 요청하더라도 매번 동일한 객체를 돌려준다. 

