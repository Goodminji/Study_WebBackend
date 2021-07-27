# Join-query

스칼라 서브쿼리 : Select 절에서 함수처럼 사용하는 쿼문을 말하며 반환값은 한개 이다. 

인라인 뷰: FROM 절에서 임시공간에 테이블을 생성하여 사용하는 와 비슷한 형

```text
select a
      ,b
      ,c 
      //스칼라 서브쿼리 
      ,(select d from tableB where tableA.a = tableB.a) as d 
from tableA 
     , (select a,b,c from tableC) tableC //인라인  
```



