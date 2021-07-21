# DTO/ENTITY/VO

**DTO** - JSON 으로 매칭 되는 것으로 URL 화면과 소통하는 데이터\(화면 데이터 파라미터,또는 리턴\)

```text
public class EmailRequest {
   private String email;
   protected EmailRequest() {}
}
```

* RequestBody 로 데이터 받을때 기본생성자가 있어야 생성이 가능. \( 또는 set\)
* protected 선언은 사용자가 직접 사용해서 선언하지 않게 하기 위해서.. 
* 보통 DTO은 setter 가 없고 getter 만 사용 

**ENTITY**

* 엔티티에는 테이블 쿼리하고 매칭이되며 로직이 들어감\(validation같은..\)
* 식별이 가능해야하고 시간의 흐름에 따라 변경이 가능하다. \(equals, hashCode 재정의\)

**VO**

* 불변의 객체 \( 돈 단위, 주소 :시/군/구  같은 불변의 객체\) ,  비즈니스로직 포함

