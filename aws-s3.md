# AWS S3

1. 개념 

* 단순한 웹 서비스 인터페이스를 사용하여 언제든지 웹상 어디서나 원하는 양의 데이터를 저장하고 검색.
* 버킷에 데이터를 무한정으로 저장. Amazon S3 버킷에 객체를 원하는 만큼 업로드할 수 있으며, 각 객체에 최대 5TB의 데이터를 포. 각 객체는 고유한 개발자 할당 키를 사용하여 저장 및 검색. 
* buket 버킷  - 버킷은 Amazon S3에 저장된 객체에 대한 컨테이너 , Amazon S3 생성하는 최상위 폴더 
* Objects - Amazon S3에 저장되는 기본 객. 객체는 객체 데이터와 메타데이터로 구성. 키가 객체의 이름이며  값이 객체의 데이터
* Keys - 키는 버킷 내 객체의 고유한 식별자
* Regions - 객체가 저장되는 물리적 위치이며 리전간 객체 공유 불가. 지연 시간 최적화, 비용 최소화, 규정 요구 사항 준수 등 다양한 필요에 따라 리전을 선택  
*  `https://doc.s3.amazonaws.com/2006-03-01/AmazonS3.wsdl`이라는 URL에서 “`doc`”는 버킷의 이름이고 “`2006-03-01/AmazonS3.wsdl`”은 키
* AWS S3연동은 Network I/O Bound 처리 이기 때문에 언제든 예외가 발생할 수 있음을 고려 해야 한다. 

2. AWS 사용

* pom.xml 등록 

```text
  <dependency>
      <groupId>com.amazonaws</groupId>
      <artifactId>aws-java-sdk-s3</artifactId>
      <version>1.11.1007</version>
    </dependency>
```

* applcation.yml 설정 

```text
cloud:
  aws:
    credentials:
      accessKey: IAM 사용자 엑세스 키
      secretKey: IAM 사용자 비밀 엑세스 키
    s3:
      bucket: 버킷 이름
    region:
      static: S3를 서비스할 region 명
    stack:
      auto: false
```

* bean 설

```text
  @Bean
  public AmazonS3 amazonS3Client(AwsConfigure awsConfigure) {
    return AmazonS3ClientBuilder.standard()
      .withRegion(Regions.fromName(awsConfigure.getRegion()))//region을 설정
      .withCredentials( //자격증명을 통해 S3 Client 가져오
        new AWSStaticCredentialsProvider(
          new BasicAWSCredentials( // 자격증명 객체
            awsConfigure.getAccessKey(),
            awsConfigure.getSecretKey())
        )
      )
      .build();
  }
```

* controller 작

```text
@PostMapping(path = "user/join", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
 public String join(
    @RequestPart(required = false) MultipartFile file
  ) throws Exception {
	  
	  
	   .....
	   s3Service.upload(file);
  }  
```

[https://docs.aws.amazon.com/ko\_kr/AmazonS3/latest/userguide/Welcome.html\#CoreConcepts](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/Welcome.html#CoreConcepts)

