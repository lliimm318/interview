# spring 의존성 주입

spring에서 의존성 주입 방법은 setter 주입, 필드 주입, 생성자 주입 이 있다.

## Spring DI

의존 관계란 A가 B를 의존할 때 의존 대상인 B가 변할 시 A에게 영향을 미치는 것을 말한다. DI(Dependency Injection)는 의존관계 주입의 약자이다.

자바에서 new 연산자를 사용해서 *Test test = new Test();* 형태로 객체를 생성한다. 
이와 다르게 DI는 저 코드처럼 객체를 생성시키는 것이 아닌, 외부에서 객체를 생성 후 주입시켜준다 !

spring 에서 DI는 외부에서 생성된 객체 중 필요한 객체를 **연결**하는 것! (필요한 객체를 해당 .java 파일 안에서 new 연산자를 통해 생성하지 않음)

### Field Injection 필드 주입

필드에 바로 의존 관계를 주입하는 방법 -> 추천하지 않음 !

~~~ java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

}
~~~

> 요렇게 쓰면 intelliJ에서 warring 나와용

#### 장점 

- 코드가 간결해짐 (과거에 많이 사용)

#### 단점

- 외부에서 접근 불가능
  - 

- 변경 불가능한 상태로 선언 가능
  - 생성자의 파라미터를 통해 의존 관계를 한눈에 파악하고 
