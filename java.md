# JAVA

1. java의 함수\(method\) 일급 객체가 아니다

* 변수에 할당되어야함
* 함수의 인자로 사용되어야
* 함수의 반환값으로 사용되어야

      java의 object는 일급 객체다 \(위 3가지 해당\)

    2. Equal hashcode 차이점

*  Equal 같으면 hashcode 같아야 한다.
* Hashcode 같으면 equal 같지 않을 수가 있다 hashcode가 충돌 되었을 수도 있고 다른 오브젝트에서도 동일한 hashcode가 생길수 있음.

