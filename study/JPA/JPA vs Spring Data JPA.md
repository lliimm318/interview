# JPA VS Spring Data JPA
솔직히 처음엔 나도 저 둘을 같다고 생각했다. (JPA를 길게 쓰면 Spring Data JPA인가..? 멍청한 과거의 나..

**둘은 다르다!!!!**

## JPA는 기술 명세이다

 JPA는 Java Persistence API의 약자이다. JPA는 단순히 명세이기 때문에 구현이 없다. JPA는 특정 기능을 하는 라이브러리가 아니고 **인터페이스**이다!

 자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스이다.
 
 JPA를 정의한 javax.persistence 패키지의 대부분은 interface, enum, Exception, 그리고 각종 Annotation으로 이루어져 있다. JPA의 핵심이 되는 EntityManager는 javax.persistence.EntityManager 라는 파일에 interface로 정의되어 있다.

~~~ java
package javax.persistence;

import ...

public interface EntityManager {

    public void persist(Object entity);

    public <T> T merge(T entity);

    public void remove(Object entity);

    public <T> T find(Class<T> entityClass, Object primaryKey);

    // More interface methods...
}
~~~

## Hibernate는 JPA의 구현체이다. 
jpa를 사용하기 위해서는 JPA를 구현한 Hibernate, EclipseLink, DataNucleus 같은 ORM 프레임워크를 사용해야 한다.
(Hibernate가 가장 범용적으로 다양한 기능을 제공해서 Hibernate를 가장 많이 쓴다.)

Hibernate는 JPA라는 명세의 **구현체**이다. 즉, 위에서 언급한 javax.persistence.EntityManager와 같은 인터페이스를 직접 구현한 라이브러리이다. 
JPA와 Hibernate는 마치 자바의 interface와 해당 interface를 구현한 class와 같은 관계이다. 

![image](https://user-images.githubusercontent.com/66578746/232967339-874551b7-275e-437d-b009-402052636f22.png)

JPA와 Hibernate의 상속 및 구현 관계이다.
JPA의 핵심인 EntityManagerFactory , EntityManager , EntityTransaction을
Hibernate에서 SessionFactory , Session , Transaction 으로 상속 받아 구현하고 있다.


![image](https://user-images.githubusercontent.com/66578746/232967315-c268f1ab-daa1-43ba-9142-f76cfeda99db.png)

SQL을 사용하지 않고 직관적인 코드(메소드)를 사용해 데이터를 조작이 가능하다.
SQL을 직접 사용하지 않는다고 JDBC를 사용하지 않는 것은 아니다.
Hibernate 안에는 JDBC API가 동작하고 있다. 단지 개발자가 직접 SQL을 작성하지 않는 것이다.
 
### 장점
**생산성** <br/>
메소드 호출만으로 쿼리가 수행된다. (SQL을 직접 사용하지 않음)
즉, 반복적인 SQL과 CRUD 작업을 하지 않아 생산성이 증가한다.

**유지보수**<br/>
컬럼이 변경 되었다면, Mybatis에서는 관련 부분을 수정해야 하지만, JPA를 사용하면 JPA가 이를 해주기에 유지보수에 좋다. 

**객체지향적이다**<br/>
로직을 쿼리에 집중하지 않고 객체 자체에 집중할 수 있다. 
객체지향적으로 데이터를 관리할 수 있기 때문에 비지니스 로직에 집중 가능하다.

**종속적이지 않다** <br/>
여러 DB(MySQL, MariaDB.. 등) 마다 SQL 사용이 조금씩 다르기에 DB를 변경하면 수정하는데 많은 시간이 걸려 교체하기 쉽지 않다.
하지만 JPA는 추상화된 데이터 접근 계층을 제공해서 특정 DB에 종속적이지 않다. 설정 파일에서 JPA에게 어떤 DB를 쓰는지 알려주기만 하면 된다!

### 단점

**어렵다** <br/>
잘 이해하지 않고 사용하면 데이터 손실이 있을 수 있다.
많은 내용이 추상화 되어있어서 JPA를 사용하기 위해 알하야할 것이 많다.

**성능** <br/>
메소를 통해 쿼리를 사용하는 것은 내부적으로 많은 동작이 있다. 
그래서 직접 SQL을 실행하는 것보다 성능이 떨어질 수 있다. (그러나 지금은 많이 발전하고 있고, 좋은 성능을 보여주고 있다.)

**세밀함** <br/>
메소를 통해 쿼리를 사용하기에 세밀함이 떨어진다.
객체 간의 매핑이 잘못 되었거나, JPA를 잘못 사용하면 다른 결과를 불러올 수 있다. <br/>
복잡한 통계 분석 쿼리를 JPA로 처리하기엔 무리가 있다. 
그래서 SQL 자체 쿼리를 작성할 수 있도록 지원도 하고 있다. (SQL과 유사한 JPQL을 지원한다)

## Spring Data JPA
Spring에서 제공하는 라이브러리로, JPA를 쉽게 

 
 
