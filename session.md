# Session

### Session 기반 인증

* HTTP는 무상태 프로토콜이고 어떤 정보도 저장하지 않음
* 클라이언트는 HTTP 요청에 session-id를 포함시켜 서버가 클라이언트를 식별.
* Session은 서버 메모리상에 저장되고 서버 메모리를 사용하기 때문에 너무 많아질 경우 서버 메모리 부족.
* 서버 장애시 Session 정보 유실
* 브라우저에 쿠키로 session-id를 저장한다.
* 쿠키에 있는 sessionid 하고 서버 메모리에 있는 sessionid를 비교 하여 검증한다.
* [https://mohwaproject.tistory.com/entry/HTTP-Session-%EC%9D%B4%EB%9E%80](https://mohwaproject.tistory.com/entry/HTTP-Session-%EC%9D%B4%EB%9E%80)
* [https://jins-dev.tistory.com/entry/Session-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EA%B3%BC-Token-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D](https://jins-dev.tistory.com/entry/Session-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EA%B3%BC-Token-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D)

### Session Cluster

* 조회 속도와 안정성을 위해 보통 In-Memory 분산 데이터베이스 사용
* 세션 공유 
* 특정 서버에 문제가 생겨도 다른 정상적인 서버에서 Session 가져올 수 있음
* Session 저장하기 위해 별도의 데이터 베이스 필요
*  Session Cluster 문제시 대규모 장애 발생 가능성이 큼

