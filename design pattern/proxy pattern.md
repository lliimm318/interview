# 프록시 패턴
프록시는 대리인이라는 뜻으로, 무언가를 대신 처리하는 의미이다.<br/> 
프록시 패턴은 어떤 객체에 대한 접근을 제어하는 용도로 대리인에 해당하는 객체를 제공하는 패턴이다. 일종의 비서 마냥 바로 사장을 만나는 것이 아닌, 비서를 통해 사장을 만나는 개념이라고 생각할 수 있다.

어떤 객체를 사용하고 할 때, 객체를 직접 참조하는 것이 아니라 해당 **객체를 대행하는 프록시 객체를 통해 대상 객체에 접근** 하는 방식을 사용한다. 
이렇게 되면 **해당 객체가 메모리에 존재하지 않아도 기본적인 정보를 참조하거나 설정**할 수 있고, 실제 객체의 기능이 반드시 필요한 시점까지 객체 생성을 미룰 수 있다.
<br/><br>
## UML
![image](https://user-images.githubusercontent.com/66578746/228101270-785268da-5f98-4e9d-a2af-77c76942cac5.png)

<br/><br>
## 왜 쓸까?

**OCP (Open Close Principle)** <br/>
> solid 원칙의 개방 폐쇄 원칙을 지킬 수 있다. (확장에 대해서는 개방적(open)이고, 수정에 대해서는 폐쇄적(closed))

기존 코드를 변경하지 않고 새로운 코드 추가가 가능하다!

**SRP (Single Responsibility Principle)** <br/>
> solid 원칙의 단일 책임 원칙을 지킬 수 있다. (객체는 단 하나의 책임(기능)만 가져야 한다)

기존 코드가 해야하는 일만 유지할 수 있다.

**유연한 코드**
객체 초지화 지연 및 기능 추가(로깅 캐싱 등등), 흐름 제어 등으로 다양하게 활용 가능하다.
<br/><br>
## 예제
``` java
public interface Cat {
    void bark();
}
```
``` java
public class Ragdoll implements Cat {
 
    @Override
    public void bark() {
        System.out.println("야옹");
    }
}
```
``` java
public class Proxy implements Cat {
 
    private Cat cat;
 
    @Override
    public void bark() {
        // 객체의 초기화를 지연시켜 실제로 사용될 때 생성함으로써 메모리 절약 가능
        if (this.cat == null) {
            this.cat = new Ragdoll();
        }
 
        cat.bark(); // 프록시가 Ragdoll()의 메소드를 호출한다.
    }
}
```
``` java
public class Main {
    public static void main(String[] args) {
        // Ragdoll 클래스의 메소드를 호출하는것이 아닌 Proxy 클래스의 메소드를 호출한다.
        Cat cat = new Proxy();
        cat.bark(); // 내부적으로 Ragdoll의 메소드를 호출한다.
    }
}
```
Main에서 Ragdoll 클래스에 직접 접근하지 않고, Proxy를 생성하여 대신 시킨다. 프록시는 bark 메소드를 호출하고 그 리턴 값을 Main에 반환한다.
<br/><br>
## 장점과 단점
### 장점
- 기존 객체를 수정하지 않고 프록시 패턴을 통해 추가 가능하다.
- 실제 객체를 수행하기 전ㄴ에 전처리를 하거나, 기존 객체를 캐싱 가능하다 (기존 객체 리소스가 무거울 경우 캐싱을 통해 부하를 줄일 수 있다.)
- 로컬에 있지 않고 떨어져 있는 객체를 사용할 수 있다. 

### 단점
- 코드의 복잡성이 증가한다. 로직이 난해해져서 가독성이 떨어질 수 있다.
- 성능이 저하될 수 있다. 객체 생성 시에 한 단계를 거쳐서 빈번한 객체 생성이 필요하 경우나 객체 생성을 위해 수레드 생성 및 동기화가 구현되어야 하는 경우 성능이 떨어질 수 있다.

