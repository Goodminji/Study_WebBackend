# HandlerMethodArgumentResolver - paging

HandlerMethodArgumentResolver 이용.

HandlerMethodArgumentResolver 인터페이스의 역할은 컨트롤러에서 파라미터를 바인딩 해주는 역할을 한다. 예를 들어 특정 클래스나 특정 어노테이션등의 요청 파라미터를 수정해야하거나, 또는 클래스의 파라미터를 조작 혹은 공통적으로 써야하는 파라미터들을 바인딩 해주는 역할이다.

* parameter로 받는 값이 여러 개가 존재하고\(혹은 객체의 필드들이 여러 개가 존재\), 그것을 처리하는 코드들의 중복이 발생할 때
* Controller에 공통으로 입력되는 parameter들을 추가하거나 수정하는 등의 여러 공통적인 작업들을 한 번에 처리하고 싶을 때



HandlerMethodArgumentResolver 설정

* 사용자의 요청이 Controller 가기 전에 HandlerMethodArgumentResolver 타서 그 요청에 대한 파라미터 수정해준다.

```text
public class PageableMethodArgumentResolver implements HandlerMethodArgumentResolver{
	
	private PageableRequest pageableRequest;

	public PageableMethodArgumentResolver(PageableRequest pageableRequest) {
		this.pageableRequest = pageableRequest;
	}
	
	//  supportsParameter : 바인딩할 클래스를 지정해주는 메서드. Pageable 클래스.
	@Override
	public boolean supportsParameter(MethodParameter parameter) {
		return Pageable.class.isAssignableFrom(parameter.getParameterType());
	}

	// resolveArgument : 바인딩할 객체를 조작할 수 있는 메서드
	@Override
	public Object resolveArgument(MethodParameter parameter, ModelAndViewContainer mavContainer,
			NativeWebRequest webRequest, WebDataBinderFactory binderFactory) throws Exception {
		
		String offsetString = webRequest.getParameter("offset");
		String limitString = webRequest.getParameter("limit");
		
		return new PageableRequest(offset,limit);
	}
}
```

* HandlerMethodArgumentResolver를 설정\(Configuration\)에 등록. WebmvcConfigurer라는 인터페이스의 addArgumentResolver\(\) 메서드에 등

```text
@Configuration
public class WebMvcConfigure implements WebMvcConfigurer {

  // TODO offset,limit를 Query Parameter로 받아 Pageable 구현체를 생성해주는 HandlerMethodArgumentResolver 인터페이스 구현체 설
  
  @Override
  public void addArgumentResolvers(List<HandlerMethodArgumentResolver> argumentResolvers) {
	  argumentResolvers.add(new PageableMethodArgumentResolver(new PageableRequest()));
  }
  ........
}
```



* - controller에서 parameter가 Pageable 타입이면 해당 작업을 수행할 것이며, 

  - 요청 URL의 parameter로 들어온 offset과 limit의 값을 적절하게 조작하고, PageRequest 객체를 리턴한다  

```text
  @GetMapping(path = "user/{userId}/post/list")
  public ApiResult<List<PostDto>> posts(
    ....
    ,Pageable pageable
  ) {
    System.out.println(pageable.offset());
    System.out.println(pageable.limit());
    ..
  }
  
  // 쿼리에서 offset, limit 사용 가능
    "SELECT * FROM posts p  
     ORDER BY p.seq DESC 
     LIMIT ? OFFSET ?"
```

출처 : [https://jhkang-tech.tistory.com/49](https://jhkang-tech.tistory.com/49)

출처: [https://starkying.tistory.com/entry/Spring-MVC-—-HandlerMethodArgumentResolver-사용하기](https://starkying.tistory.com/entry/Spring-MVC-%E2%80%94-HandlerMethodArgumentResolver-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0) \[Random Access Memories\]

