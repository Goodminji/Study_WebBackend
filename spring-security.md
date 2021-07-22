# Spring Security

  
1. SecurityContext : 접근 주체와 인증정보를 담고있는 Context,,, securityContextholer 를통해 접근. securityContextholer 는 어디서든지 불러서 사용할 수 있는데 ThreadLocal에 보관 \(threadLocal 이란 해당 스레드에 고유 저장 영역, 해당 스레드를 실행하면 언제든지 사용 가능한 공간\)

2.  주요 필터

* SecurityContextPersistenceFilter : SecurityContextRepository 에서 SecurityContext 를 로딩하거나 SecurityContextRepository 로 SecurityContext 를 저장하는 역할을 한다.
* LogoutFilter : 로그아
* UsernamePasswordAuthenticationFilter : 아이디와 비밀번호를 사용하여 사용자 인
* ExceptionTranslationFilter : 예외 처
* filterSecurityInterceptor:  AccessDecisionManager 로 권한부여 처리를 위임함으로써 접근 제어 결정을 쉽게해준다.

3. 인증 흐름 : 현재 사용자가 누군지 식별\(Authenticate\)

*  UsernamePasswordAuthenticationFilter 처음 요청 하고 인증 안된 사용자 정보\(Authentication\) 를 가져 온다\(id, password\) =&gt; authenticationManager에게 정보를 넘겨주고 Manager는 authenticationProvider를 실행한다. =&gt; provider가 리스트로 가지고 있는데 supports 로 적절한 인증처리 방법이 있는지를 체크하여 provider를 선택한다. =&gt; 인증 처리를 수행 =&gt; 인증된 Authentication 를 반환한다.
*   UsernamePasswordAuthenticationFilter : http요청에서 사용자 ID, 비밀번호 추출 , UsernamePasswordAuthenticationToken생성
* UsernamePasswordAuthenticationToken : 사용자 인증 요청을 Authentication 인터페이스 구현체 \( 인증전/인증후\)
* AuthenticationManager : 사용자 비밀번호  인증하는 역할 , 실패시 Authentication

  exception 

* AuthenticationProvider : 실질적인 사용자 인증처리 로직, 인증결과 UsernamePasswordAuthenticationToken 리턴.

4. 인가 : 현재 사용자가 보호된 리소스에 권한이 있는지 검사\(autorize\)

* AccessDecisionManager : 인증된 사용자의 보호 리소스 접근 여부를 판단\(AffirmativeBased : 접근 승인하는 Voter가 1개 이상                          ConsensusBased: 과반수                                                                  unanimouseBased: 모든 Voter가 승인해야함\)
* AccessDecisonVoter : AccessDecisionManager은 다수의 AccessDesiconVoter로 구성 , 각각의 Voter는 승인,거절, 보류 를 반환                                                              - **Grant\(ACCESS\_GRANTED\)** : Voter 가 리소스에 대한 접근 권한을 허가하도록 권장한다.                                                                                                                                  - **Deny\(ACCESS\_DENIED\)** : Voter 가 리소스에 대한 접근 권한을 거부하도록 권장한다.                                                                                                                                      - **Abstain\(ACCESS\_ABSTAIN\)** : Voter 는 리소스에 대한 접근권한 결정을 보류한다. 이 결정 보류는 다음과 같은 경우에 발생할 수 있다.  출처: [https://springsource.tistory.com/80](https://springsource.tistory.com/80) \[Rednics Blog\] [https://www.slideshare.net/madvirus/ss-36809454](https://www.slideshare.net/madvirus/ss-36809454)[https://hyunsangwon93.tistory.com/27?category=746259](https://hyunsangwon93.tistory.com/27?category=746259)

[https://springsource.tistory.com/80](https://springsource.tistory.com/80)

