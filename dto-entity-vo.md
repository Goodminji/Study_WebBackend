# DTO/ENTITY/VO

**DTO** - JSON 으로 매칭 되는 것으로 URL 화면과 소통하는 데이터\(화면 데이터 파라미터,또는 리턴\)

데이터가 포함된 객체를 한 시스템에서 다른 시스템으로 전달하는 작업을 처리하는 객체입니다. Vo와 dto의 차이점은 vo는 특정한 비즈니스 값을 담는 객체를 vo라 하고 dto는 레이어간의 통신용도로 오가는 객체를 dto라고 합니다.

Vo와 DTO의 비교

DTO는 메소드 호출 횟수를 줄이기 위해 데이터를 담고 있는 녀석으로, VO는 값이 같으면 동일 오브젝트라고 볼 수 있는 녀석으로 표현을 하고 있습니다.  


```text
public class EmailRequest {
   private String email;
   protected EmailRequest() {}
}
```

* RequestBody 로 데이터 받을때 JSON 형태 이어야 하므로 기본생성자가 있어야 생성이 가능. \( 또는 set\)
* protected 선언은 사용자가 직접 사용해서 선언하지 않게 하기 위해서.. 
* 보통 DTO은 setter 가 없고 getter 만 사용 

**ENTITY**

* 엔티티에는 테이블 쿼리하고 매칭이되며 로직이 들어감\(validation같은..\)
* 식별이 가능해야하고 시간의 흐름에 따라 변경이 가능하다. \(equals, hashCode 재정의\)

**VO**

* 불변의 객체 \( 돈 단위, 주소 :시/군/구  같은 불변의 객체\) ,  비즈니스로직 포함
* Value Object는 DTO와 동일한 개념이나 차이 점은 read only 속성을 갖습니다.

  Value Object는 관계데이터베이스의 레코드에 대응되는 자바클래스입니다. 형태는 db레코드를 구성하는 필드들을 Value Object의 Attribute로 하고 해당 변수에 접근 할 수 있는 Getter Setter 메소드의 조합으로 클래스를 형성되어진 클래스입니다. 특성은 대체로 불변성이고 equals\(\)로 비교할 때 객체의 모든 값을 비교해야 합니다.  

