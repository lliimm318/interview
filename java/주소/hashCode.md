# hashCode

객체의 주소 값을 이용해서 해싱 기법을 통해 해시 코드를 만든 후 반환한다.

**객체의 주소 값이 아님!! 주소 값으로 만든 고유한 숫자 값**

~~~ java
class Person {
    String name;

    public Person(String name) {
        this.name = name;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("홍길동");
        Person p2 = new Person("홍길동");

        // 객체 인스턴스마다 각기 다른 해시코드(주소))를 가지고 있다.
        System.out.println(p1.hashCode()); // 622488023
        System.out.println(p2.hashCode()); // 1933863327
    }
}
~~~

## equals

equals의 결과가 같다면 해시 코드가 같아야 함. equals의 결과가 다르다면 다른 해시코드를 반환할 필요는 없지만, 다르면 성능이 좋음 !

equals와 해시 코드는 같이 재정의 하라고 한다 ! 왜 그럴까 ?<br/>
-> 해시 기반 친구들을 사용할 때 문제가 생겨서

#### equals만 재정의

위에서 "equals의 결과가 같다면 해시 코드가 같아야 함" 이라고 말했다
equals만 오버라이딩 시 해시코드가 달라서 같은 객체로 판단된다. 

ex) HashSet 사용 시 : set은 중복된 값을 허용하지 않으나 해시코드가 달라서 중복된 데이터로 취급하지 않음

<img width="701" alt="스크린샷 2024-06-13 오전 10 05 17" src="https://github.com/lliimm318/interview/assets/66578746/f72d24b0-81b5-473d-b29a-c661a3ece37b">

hashMap, Hashset, 등은 객체가 논리적으로 같은지 비교할 때 해시 리턴 값이 같은지 비교 후 equals 리턴 값을 비교한다.
그래서 해시 값이 다르면 다른 값으로 친다.

## 해시 코드는 고유할까?

자바는 포인터를 철저하게 숨겨 직접적인 객체의 주소 값을 얻을 수 없다, 그래서 자바는 주소값을 표현하기 위해 해시 코드를 이용한다

그럼 해시 코드는 고유할까 ? 아니다. **hashCode() 메서드가 int형 정수를 반환하기 때문이다**

서로 다른 객체라도 같은 해시 코드가 반환될 수 있따 !!!!!

### 해시 충돌

요즘 64비트 컴퓨터에서 돌아가는 JVM은 기본적으로 8바이트 (64비트) 주소 체계를 기본으로 한다. 
만약 8바이트의 해시코드를 이용해 반환하면 메소드 타입에 따라 4바이트로 강제 형변환 된다. (long -> int)
그래서 값이 겹칠 수도 있는 케이스가 존재한다. 

그럼 long으로 하면 안되나 ? 싶지만.. 이미 int로 여러 프로젝트에서 사용하고 있어 호환성을 위해 놔둔것


: https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EA%B0%9D%EC%B2%B4%EC%9D%98-hashCode%EB%8A%94-%EA%B3%A0%EC%9C%A0%ED%95%98%EC%A7%80-%EC%95%8A%EB%8B%A4-%E2%9D%8C
