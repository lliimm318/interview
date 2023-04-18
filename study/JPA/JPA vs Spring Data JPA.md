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
 Hibernate는 JPA라는 명세의 **구현체**이다. 즉, 위에서 언급한 javax.persistence.EntityManager와 같은 인터페이스를 직접 구현한 라이브러리이다. 
 JPA와 Hibernate는 마치 자바의 interface와 해당 interface를 구현한 class와 같은 관계이다. ORM의 프레임 워크기도 하다!


 
 
