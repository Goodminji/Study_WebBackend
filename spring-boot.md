# Spring boot

1.     스프링 부트 의 장점

*   Packaging Executable Jar
* 테스트 환경과 내장 tomcat
* start 를 제공. 
* Auto configuration

  스타터를 이용해 라이브러리의 의존성 버전을 권장버전으로 자동 설정 

2.     기본적으로 Spring boot dependency 부모로 상속하여 사용.

              \( 스프링 버전  자동으로 설정 되어있음\)

```text
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.5.1</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
```

3.     Spring bootApplication 어플리케이션 메인 클래스 자동 생성



```text
@SpringBootApplication
public class toyApplication {
       public static void main(String[] args) {
               SpringApplication.run(toyApplication.class, args);
       }
}
```

