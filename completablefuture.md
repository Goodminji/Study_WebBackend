# CompletableFuture

### CompletableFuture 비동기 처리. 

### 대표 함수 

1. CompletableFuture.supplyAsync : 반환 값이 필요할

```text
CompletableFuture.supplyAsync(()->{
  return "";
});
```

  2. CompletableFuture.runAsync : 반환 값이 필요 없을

```text
CompletableFuture.runAsync(()->{
   System.out.println("");
});
```

3. thenAccept 비동기 작업이 완료 되었을때  완료 결과를 사용하기 

```text
CompletableFuture.supplyAsync(()->{
  return "data";
}).thenAccept((data) -> { // 리턴값이 필요 없는
   System.out.println(data);
});
```

4. thenApply 비동기 작업이 완료 되었을때  완료 결과를 새로운 값으로 다시 변환

```text
  CompletableFuture.supplyAsync(()->{
		  return "data";
		}).thenApply((data) -> { // 리턴값이 필요 
		   return data.toUpperCase(); 
		});
```

5. allof -  모든 비동기 작업을 완료 하고 모든 작업 완료 후 실행

6. anyof - 모든 비동기 작업을 완료 하고 하나만 작업이 완료되면 실행 

7. exceptionally 비동기 작업 예외가 발생 했을때 throwable 예외 처리 발생..

```text
CompletableFuture.supplyAsync(()->{
		  return "data";
		}).thenAccept((data) -> { // 리턴값이 필요 없는
      System.out.println(data);
   }).exceptionally(throwable -> {
        log.error("Unexpected error occurred: {}", throwable.getMessage());
        return emptyList();
  });
```

출처 

[https://brunch.co.kr/@springboot/267](https://brunch.co.kr/@springboot/267)

[https://www.hungrydiver.co.kr/bbs/detail/develop?id=2](https://www.hungrydiver.co.kr/bbs/detail/develop?id=2)

[https://m.blog.naver.com/2feelus/220714398973](https://m.blog.naver.com/2feelus/220714398973)



