# ControllerAdvice

ControllerAdvice 

* Controller 대상으로 공통 코드를 작성 할수 있게 도와주는 AOP 어노테이션
* controller에서 throw 하는 예외에 대해 공통 처리를 수행하기 좋은 포인트
*  @ExceptionHandler 어노테이션을 사용하여 예외를 처리할 클래스를 정의한다. \( 기본클래스는 모두 상속되거나 확장된 클래스를 처리할 것이다\) 

```text
// TODO REST API 처리 중 발생한 예외를 catch 하고, 로그를 남기고, 오류 응답을 전달

  @ExceptionHandler(value = ServiceRuntimeException.class)  
  public String serviceRuntimeException(ServiceRuntimeException e){
	  // NotFoundException
	  log.error(e.getMessage(),e);
	  if (e instanceof NotFoundException) {
		  return e.getMessage() + "Httpstatus : " + HttpStatus.NOT_FOUND;
	  }
	  else { // UnauthorizedException
		  return e.getMessage() + "Httpstatus : " + HttpStatus.UNAUTHORIZED;  
	  }
  }
  
  @ExceptionHandler(value = {IllegalStateException.class,IllegalArgumentException.class,TypeMismatchException.class,MissingServletRequestParameterException.class,JSONException.class})  
  public String badRequestException(Exception e){
	  // 400 status.BAD_REQUEST
	  log.error("BAD_REQUEST "+e.getMessage(),e);
	  return e.getMessage() + "Httpstatus : " + HttpStatus.BAD_REQUEST;  
}
@ExceptionHandler(value = HttpMediaTypeException.class)  
  public String unsupportedMediaTypeException(HttpMediaTypeException e){
	  // 415 status.UNSUPPORTED_MEDIA_TYPE
	  log.error("UNSUPPORTED_MEDIA_TYPE " +e.getMessage(),e);
	  return e.getMessage() + "Httpstatus : " + HttpStatus.UNSUPPORTED_MEDIA_TYPE;  
  }

```



* 출처: [https://springboot.tistory.com/33](https://springboot.tistory.com/33) \[스프링부트는 사랑입니다\]



