# 생성자 this()와 참조변수 this.
this() 생성자이고, this.는 자기 자신을 가르키는 참조변수이다.

## 생성자 this() 
- 같은 클래스에서 다른 생성자 호출 시 사용.   
- 다른 생성자 호출 시 첫 줄에서만 사용 가능

``` java
class User {
    String name; // 인스턴스 변수
    int age; 
    
    User() {
        this("이름", 20); 
    }
    
    User(Intger age) {
        this("이름", age);
    }
    
    User(String name, int age) {
        this.name = name; 
        this.age = age;
    }
}
```
1. 생성자의 매개변수로 선언된 변수의 이름이 인스턴스 변수와 같을 때 인스턴스 변수와 지역변수를 구분하기 위해서 사용한다.
2. this.name은 인스턴스 변수이고, name은 매개변수로 지정된 지역변수이다. 
3. static 메소드의 경우 힙 메모리가 아니라 내부 클래스 저장공간에 저장된다. 그래서 객체 생성을 하지 않아서 this()를 사용할 수 없다.
<br/></br>
## 참조변수 this.
- 인스턴스 자신을 가르키는 **참조변수**
- 인스턴스 메서드(생성자 포함)에서 사용가능
