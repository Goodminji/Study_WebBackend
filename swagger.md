# Swagger

## Swagger

* 어노테이션 기반 REST API 문서 자동화
* url: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)

### 1. 어노테이션

* @Api : controller 단위로 Rest Api 메타데이터 명시
* @ApiOperation : 하나의 rest api 요청 url에 매핑되며 문서화 대상으로 처리 됨
* @apiParam, @apilmplicitParma – Rest api 호출시 전달되는 파라미터에 대한 설명
*  @ apimodelProperty – model class 필드에 대한 설명

### 2. 설정 방법

* pom.xml 추가 

```text
<dependency>
      <groupId>io.springfox</groupId>
      <artifactId>springfox-swagger2</artifactId>
      <version>2.9.2</version>
    </dependency>

    <dependency>
      <groupId>io.springfox</groupId>
      <artifactId>springfox-swagger-ui</artifactId>
      <version>2.9.2</version>
    </dependency>
```

* SwaggerConfig 설정 

```text
@Configuration
@EnableSwagger2
public class SwaggerConfigure implements WebMvcConfigurer {

  @Bean
  public Docket restApi() {
    return new Docket(DocumentationType.SWAGGER_2)
      .select()
      // 스웨그 적용할 클래스
        .apis(withMethodAnnotation(ApiOperation.class))
      .build();
  }

}
```

* 예제 

```text
@Api(tags = "API 설명")
public class UserRestController {

private final UserService userService;

  public UserRestController(UserService userService) {
    this.userService = userService;
  }

  @PostMapping(path = "user ")
  @ApiOperation(value = "이름 확인 (API 토큰 필요없음)- 메소드 설명")
  public ApiResult<Boolean> checkName(
    @RequestBody @ApiParam(value = "example: {\"name\": \"1234\"}") Map<String, String> request
  ) {
    ……
    }
  ..
}

public class UserDto {

@ApiModelProperty(value = "사용자명", required = true)
  private String name;
  …
}

```

출처

[https://yookeun.github.io/java/2017/02/26/java-swagger/](https://yookeun.github.io/java/2017/02/26/java-swagger/)



