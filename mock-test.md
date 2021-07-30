# Mock test

**Mockito란?**

* 유닛 테스트를 위한 Java mocking framework
* 자바 단위테스트에서 가짜 객체를 지원해주는 프레임워크
* 즉, 단위 테스트를 하기 위해 Mock을 만들어주는 프레임워크
* Mock 객체 생성, Mock 객체 동작을 지정, 그리고 테스트 대상 로직이 제대로 수행 되었는지 확인 가능

```text
@ExtendWith(MockitoExtension.class)
class dd {
 
	@Autowired
	private MockMvc mockMvc;
	
	@InjectMocks
	UserController userController;
	
	@Autowired
	ObjectMapper objectMapper;
	
	//Mock 객체를 생성한다.
	@Mock
	UserService serivce;
	
	User user;

	@BeforeEach
	void beforeEach(){
		    // UserController를 Mockmvc 객체로 생성.
	     	//standaloneSetup 한개의 컨트롤러에 집중하여 테스트 하는 용도. 
			mockMvc = MockMvcBuilders.standaloneSetup(userController)
				.alwaysExpect(status().isOk())
				.build();

		user = new User(1L, "ww2@naver.com", "ww2");
	
	}
	
	@Test
	public void userJoinSave() throws Exception{
		
		objectMapper = new ObjectMapper();
		
		UserRequestDto userRequestDto = new UserRequestDto("ss@naver.com","ss");
		
		//when 메소드를 통해 하나의 메소드가 호출 되었을때 특정 값을 리턴한다.특정 조건을 지정
		// 매개변수가 어떤 값이라도 상관이 없다면 any 메소드 사용 . 특정값을 넣어야 한다면 eq() 사용
		when(serivce.userJoin(Mockito.any())).thenReturn(userResponseDto);
		
		//mockMvc를 수행하고 
		//perform에는 post/get/put/delete 사용 가능
		mockMvc.perform(post("/api/users/join")
				// 파라미터 objectMapper
                .content(objectMapper.writeValueAsString(userRequestDto))
                .contentType(MediaType.APPLICATION_JSON_UTF8)
                .accept(MediaType.APPLICATION_JSON_UTF8))
		//상태값은 OK
		.andExpect(status().isOk())
		//예상값 검증
		.andExpect(jsonPath("$.success",is(true)))	
		.andExpect(jsonPath("$.response",is("가입완료")))	
		//처리 내용을 출력한다.
		.andDo(print());
		// andReturn() 객체의 결과를 받을때 사용
	}
	
  @Test
	public void getUserIdToInfo() throws Exception{
		
		when(serivce.findbyID(Mockito.eq(1L))).thenReturn(user);
		
		mockMvc.perform(get("/api/users/1"))
		.andExpect(status().isOk())
		.andExpect(jsonPath("$.email",is("ww2@naver.com")))
		.andDo(print());
	}
 
}
```

  
  
출처: [https://www.crocus.co.kr/1556?category=395790](https://www.crocus.co.kr/1556?category=395790) \[Crocus\]    [https://jdm.kr/blog/165](https://jdm.kr/blog/165)

{% embed url="https://twofootdog.github.io/Spring-Spring-MVC%EC%97%90%EC%84%9C-JUnit-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B02\(MockMvc%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-Controller-%ED%85%8C%EC%8A%A4%ED%8A%B8\)/" %}

{% embed url="https://jdm.kr/blog/222" %}



