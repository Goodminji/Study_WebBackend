# 단위테스트 JUNIT5

단위테스트\(Junit\) 자바용 단위테스트 도구

* @Test 메소드가 호출 할때마다 새로운 인스턴스를 생성하여 독립적인 테스트가 이루어 진다. 단정\(assert\) 메소드로 테스트케이스의 수행 결과를 판별. 
* assertArrayEqulas\(a,b\) 배열 A와 B가 일치함을 확인
*  assertEqulas\(a,b\) 객체 A와 B가 같은 값을 가지는지 확인한다
*  assetEqulas\(a,b,c\) 객체 A와 B가 값이 일치하는 지를 확인한다\(a :예상값,b:결과값,c:오차범위\)
*  assertSame\(a,b\) 객체 A,B가 같은 객체임을 확인한다
* assertTrue\(a\) 조건 A가 참인지 확인한다.
* assertNotnull\(a\) 객체 A가 null 아님을 확인 한다
*  @test 메소드가 선언되면 테스트 대상 메소드
*  @test\(timeout=5000\)수행시간 제한하는것으로 단위는 초
* @test\(expected=RuntimeException.class\) RuntimeException가 발생해야 테스트가 성공 그렇지 않으면 실패 
* @beforeclass, @afterclass는 해당 테스트 클래스에서 딱 한번씩만 수행하도록 지정. 
* @before,@after 해당 테스트 클래스 안에 메소드들이 테스트 되기 전 후에 각각 실행되게 하는 어노테이션

```text
@SpringBootTest
class UserServiceTest {
      @Autowired private UserService userService;
     private String name;
  private Email email;
  private String password;

  @Beforeclass
  void setUp() {
    name = "한글";
    email = new Email("test@gmail.com");
    password = "1234";
  }

  @Test
  void 가입하기() {
    User user = userService.join(name, email, password);
    assertThat(user, is(notNullValue()));
    assertThat(user.getSeq(), is(notNullValue()));
    assertThat(user.getEmail(), is(email));
 } 
  @Test 
   …
 
}

```

