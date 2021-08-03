# Spring batch

프링 배치: 대량의 데이터를 읽어 일괄 처리 , 사용자와의 상호작용 없이 반복적으로 데이터를 트랜잭션 단위로 처리할 수 있어 개발자는 데이터 처리에 대한 비즈니스 로직에만 집중.

Application -&gt; Batch core \(jobLauncher,job,step\)-&gt; Batch infrastructure\(reader,writer\)

1. Job : 배치작업이며 최소 하나의 step을 가져야 한다.. xml 또는 java로 설정 가능.

* 작업의 간단한 이름, step인스턴스의 정의 및 순서, 작업을 다시 시작할 수 잇는지 여부
* JobRunner : 외부 요청에 의해 작업 실행을 담당하는 클래스, JobLauncher의 인스턴스화
* JobInstance: 배치 처리에서 job이 실행될때 하나의 논리적 작업 실행 단위
* jobExecution: jobinstance 에 대한 한번의 실행을 나타나는 객체\(오늘 job이 실패해 내일 동일한 job이 실행하면 동일한 jobinstance, 단 jobExecution 은 다른 것\)
* jobParameters : job이 실행될때 필요한 파라미터 \(jobparamter, jobinstance는 1대1 관계\)

     2. Step: 읽기-&gt; 가공하기 -&gt; 쓰기의 묶음이며 chunck processing 이라고 부르는데 하나의 트랙잭션 단위이다.

* stepExecution : step 실행 정보.

    3.jobRepository :  배치 처리하는 과정 중 프레임워크에서 사용하는 메타데이터 정보를 엑세스 하는 클래스

    4. jobLauncher : 작업의 시작과 실행을 관리하는 인터페이스로 jobRunner에 의해 인스턴스화 되고 jobParameters 와 함께 배치를 실행하는 주체

   5. itemReader: 청크구조에서 사용되는 컴포넌트로 배치 작업에서 모든 데이터에 대한 처리가 될때까지 DB,file 등의 소스에서 반복적으로 읽는데 사용하는 인터페이스

   6. Itemprocessor  : 청크 구조에서 사용되는 컴포넌트로 reader로 읽어 온 데이터를 변환하기 위한 역할 을 수행\(필수 아님\)

   7. Itemwriter : 청크 구조에서 사용되는 컴포넌트로 배치에서 데이터를 DB,file 등에 저장하기 위한 인터페이스

