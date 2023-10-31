# factory pattern

> 객체 생성을 위한 인터페이스 정의 후 어떤 클래스이 인스턴스를 만들지 서브 클래스에서 결정하는 디자인 패턴

객체 생성 로직을 추상화하고 구체 클래스의 생성을 클라이언트로부터 분리한다. 객체 생성에 관한 복잡성을 숨기고 클라이언트 코드를 간소화할 수 있다.

## 그래서 왜 쓰는건데요

객체지향 5대원칙 solid를 보자! 
- OPC(Open Closed Principle) !!!
- 확장에 열려 있고, 수정에 닫혀 있어야한다.

수정에 닫혀 있다... 코드를 수정하지 않아도 모듈의 기능을 확장하거나 변경 가능하다를 말한다. 그래서 수정이 일어날 가능성이 큰 부분과 그렇지 않은 부분을 분리하는 것이 좋다.

객체는 속성과 함수가 변경 또는 추가될 수 있다. 이에 객체의 생성을 담당하는 코드는 변경의 가능성이 높다. 객체 생성을 담당하는 클래스를 한 곳에서 관리해서 **결합도를 줄이기 위해** 쓴다 !

다향성을 이용하여 인터페이스를 구현한 객체들은 같은 인터페이스를 상속 받아 코드가 유연하다. 객체를 생성하는 코드 부분을 분리 시켰기 때문에 객체의 수정 혹은 추가가 일어나도 객체를 생성하는 코드만 수정하면 된다

#### 결합도 ??

~~~ java
class A {
  // 대충 코드인 것
}

class B {

  A a = new A();

}
~~~

클래스 B는 A를 사용한다. 이를 의존 관계라고 말한다. 의존 대상인 A클래스가 사라지면, B는 컴파일이 불가능해지고 동작할 수 없다.

한 클래스의 변경점이 다른 클래스의 영향을 주는가를 결합도라고 말한다.

## 팩토리 메소드 패턴

![image](https://github.com/lliimm318/interview/assets/66578746/ea2f7adf-ab00-43fa-946d-0551431d54ea)

**AS IS**

product의 생성자가 바뀌면 각각의 클래스에 있는 모든 product 객체을 생성자를 변경해야한다.

------

![image](https://github.com/lliimm318/interview/assets/66578746/e48876b1-d083-40fb-829a-7cc282281a4b)

**TO BE**

객체의 생성을 담당하는 클래스를 한 곳으로 분리한다. 

팩토리 클래스에서 getInstance() 메소드를 통해 인스턴스를 반환한다. user 클래스 내부에서 Product 객체를 직접 생성하지 않는다.
팩토리 클래스에 인스터스를 요청 후 생성된 인스턴스를 반환 받는다.

Product 생성자가 변경되면? 팩토리에 getInstance() 메소드 내부의 생성자만 변경 시켜주면 된다.

![image](https://github.com/lliimm318/interview/assets/66578746/e37df015-b3e4-497e-b1a7-c0bc129d340d)

좀 더 복잡한 것...

shape 인터페이스를 만들고 해당 인터페이스를 구현하는 구체적인 클래스를 만든다!
개인적으로 내가 좋아하는 스타일이다 (예쁘자낭 😛)

### 인터페이스
~~~ java
public interface Shape {
  void draw();
} 
~~~

### 구현체
~~~ java

public class Rectangle implements shape {

  public void draw() {
    println("직사각형 직사각사각");
  }
  
}

public class Square implements shape {

  public void draw() {
    println("정사각형 정정사각각");
  }
  
}

public class Circle implements shape {

  public void draw() {
    println("동그라미 동글동글동글");
  }
  
} 

~~~

shape을 구현한 클래스들은 shape의 draw 메소드를 구현한다.

### Factory
~~~ java
public class ShapeFactory {
    public Shape getShape(String shapeType) {

        if (shapeType == null) {
            return null;
        }

        if (shapeType.equals("CIRCLE")) {
            return new Circle();
        }
        else if (shapeType.equals("RECTANGLE")) {
            return new Rectangle();
        }
        else if (shapeType.equals("SQUARE")) {
            return new Square();
        }
        
        return null;
    }
}
~~~

팩토리 클래스에서 어떤 클래스를 만들지 결정하여 **객체의 생성을 캡슐화**한다.

### 사용
~~~ java
public class Main {
    public static void main(String[] args) {
        ShapeFactory shapeFactory = new ShapeFactory();

        Shape circle = shapeFactory.getShape("CIRCLE");
        circle.draw();

        Shape rectangle = shapeFactory.getShape("RECTANGLE");
        rectangle.draw();

        Shape square = shapeFactory.getShape("SQUARE");
        square.draw();
    }
}
~~~

변수 circle, rectangle, square는 모두 생성자가 어떻게 생겼는지 모른다. 팩토리한테 "CIRCLE" 모양을 달라고 요청한 것이다.

### 펙토리 메소드 패턴 장단점

#### 장점 !
- 객체간의 결합도를 낮춤
- 단일 책임 원칙 (SOP) 코드에서 생성자 코드를 분리해서 코드를 간결하게 만들 수 있다.
- 개방 폐쇄 원칙 (OCP) 기존 클라이언트 코드를 수정하지 않고 새로운 타입을 추가 가능하다.

#### 단점 !
- 패턴을 구현할 많은 서브 클래스가 필요하다.


## 추상 펙토리 메소드 패턴

연관된 서브 클래스를 특정 그룹으로 묶어 한번에 교체할 수 있도록 만든 디자인 패턴이다.

앞에서 말한 팩토리 메소드 패턴이랑 비슷해보이지만 팩토리를 만드는 상위 팩토리 클래스가 존재한다!

![image](https://github.com/lliimm318/interview/assets/66578746/886db44c-ff0c-47f4-9ebb-e51f296c2c0a)

솔직히 임서영은 어렵다 (어렵기 보단 복잡해서 안 쓰는듯)

### 클래스 
~~~ java
class RoundedRectangle implements Shape {
    public void draw() {
        System.out.println("Inside RoundedRectangle::draw() method");
    }
}

class RoundedSquare implements Shape {
    public void draw() {
        System.out.println("Inside RoundedSquare::draw() method");
    }
}
~~~

### Super Factory 
~~~ java
interface AbstractFactory {
    Shape getShape(String shapeType);
}
~~~

### 하위 Factory 
~~~ java
class ShapeFactory implements AbstractFactory {
    public Shape getShape(String shapeType) {
        if (shapeType.equals("RECTANGLE")) {
            return new Rectangle();
        } else if (shapeType.equals("SQUARE")) {
            return new Square();
        }
        return null;
    }
}

class RoundedShapeFactory implements AbstractFactory {
    public Shape getShape(String shapeType) {
        if (shapeType.equals("RECTANGLE")) {
            return new RoundedRectangle();
        } else if (shapeType.equals("SQUARE")) {
            return new RoundedSquare();
        }
        return null;
    }
}
~~~

### Factory 를 생성하는 Producer
~~~ java
class FactoryProducer {
    public static AbstractFactory getFactory(boolean rounded) {
        if (rounded) {
            return new RoundedShapeFactory();
        } else {
            return new ShapeFactory();
        }
    }
}

~~~

### 사용
~~~ java
public class Main {
    public static void main(String[] args) {
        AbstractFactory shapeFactory1 = FactoryProducer.getFactory(false);

        Shape shape1 = shapeFactory1.getShape("RECTANGLE");
        shape1.draw();

        Shape shape2 = shapeFactory1.getShape("SQUARE");
        shape2.draw();

        AbstractFactory shapeFactory2 = FactoryProducer.getFactory(true);

        Shape shape3 = shapeFactory2.getShape("RECTANGLE");
        shape3.draw();

        Shape shape4 = shapeFactory2.getShape("SQUARE");
        shape4.draw();
    }
}

~~~

### 추상 펙토리 패턴 장단점

#### 장점 !
- 팩토리로부터 만들어진 객체들은 호환가능함을 보장할 수 있다.
- 객체간 결합도를 낮출 수 있다.
- 단일 책임 원칙 (SOP) 코드에서 생성자 코드를 분리해서 코드를 간결하게 만들 수 있다.
- 개방 폐쇄 원칙 (OCP) 기존 클라이언트 코드를 수정하지 않고 새로운 타입을 추가 가능하다.
  
#### 단점 !
- 패턴을 구현할 많은 서브 클래스가 필요하다. (복잡..

# 결론 ~
- 팩토리 메소드 패턴 : 객체를 생성하는 인터페이스를 정의 함으로써, 어떤 인스턴스를 생성할 지는 하위 클래스에서 결정하는 패턴이다.
- 추상 팩토리 패턴 : 팩토리들을 그룹으로 묶어 관리할 수 있는 패턴이다.


#### 디자인 패턴에 대한 개인적인 여담
솔직히 디자인 패턴은 이론 공부로는 한계가 있다. 직접 타자로 코드를 작성하면서 차이점을 확실하게 느껴보는 것이 중요하다. 나는 코드를 짜고 있으면서도 디자인 패턴을 이해를 못할 때가 많은데 그냥 날 잡고 디자인 패턴에 굴러야겠다. 데굴데굴ㄹ
