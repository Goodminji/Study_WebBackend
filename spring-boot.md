# Spring boot

1.     스프링 부트 의 장점

-      Auto configuration

-      Packaging Executable Jar

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

