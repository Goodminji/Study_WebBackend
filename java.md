# JAVA

1. java의 함수\(method\) 일급 객체가 아니다

* 변수에 할당되어야함
* 함수의 인자로 사용되어야
* 함수의 반환값으로 사용되어야

      java의 object는 일급 객체다 \(위 3가지 해당\)

    2. Equal hashcode 차이점

*  Equal 같으면 hashcode 같아야 한다.
* Hashcode 같으면 equal 같지 않을 수가 있다 hashcode가 충돌 되었을 수도 있고 다른 오브젝트에서도 동일한 hashcode가 생길수 있음.

   3. Lambda – 함수형 프로그래밍 기법을 지원하여 사용 가능                                                   JAVA는 일급객체를 지원하지 않기 때문에 람다 사용이 제한적                                     함수형 인터페이스\(메소드가 하나인 인터페이스\) 는 람다로 표현가능

