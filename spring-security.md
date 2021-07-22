# Spring Security

  
1. SecurityContext : 접근 주체와 인증정보를 담고있는 Context,,, securityContextholer 를통해 접근. securityContextholer 는 어디서든지 불러서 사용할 수 있는데 ThreadLocal에 보관 \(threadLocal 이란 해당 스레드에 고유 저장 영역, 해당 스레드를 실행하면 언제든지 사용 가능한 공간\)

2.  주요 필터

* SecurityContextPersistenceFilter
* LogoutFilter
* UsernamePasswordAuthenticationFilter
* ExceptionTranslationFilter
* filterSecurityInterceptor

3. 인증 흐름 : 현재 사용자가 누군지 식별\(Authenticate\)

*  UsernamePasswordAuthenticationFilter 처음 요청 하고 인증 안된 사용자 정보\(Authentication\) 를 가져 온다\(id, password\) =&gt; authenticationManager에게 정보를 넘겨주고 Manager는 authenticationProvider를 실행한다. =&gt; provider가 리스트로 가지고 있는데 supports 로 적절한 인증처리 방법이 있는지를 체크하여 provider를 선택한다. =&gt; 인증 처리를 수행 =&gt; 인증된 Authentication 를 반환한다.
*   UsernamePasswordAuthenticationFilter : http요청에서 사용자 ID, 비밀번호 추출 , UsernamePasswordAuthenticationToken생성
* UsernamePasswordAuthenticationToken : 사용자 인증 요청을 Authentication 인터페이스 구현체 \( 인증전/인증후\)
* AuthenticationProvider : 실질적인 사용자 인증처리 로직, 인증결과 UsernamePasswordAuthenticationToken 리턴.

4. 인가 : 현재 사용자가 보호된 리소스에 권한이 있는지 검사\(autorize\)

* AccessDecisionManager : 인증된 사용자의 보호 리소스 접근 여부를 판단\(AffirmativeBased : 접근 승인하는 Voter가 1개 이상                          ConsensusBased: 과반수                                                                  unanimouseBased: 모든 Voter가 승인해야함\)
* AccessDecisonVoter : AccessDecisionManager은 다수의 AccessDesiconVoter로 구성 , 각각의 Voter는 승인,거절, 보류 를 반환

