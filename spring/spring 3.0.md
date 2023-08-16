# spring 3.0

## 변경
- **Java17 이상 지원**
- **JavaEE**

  Jakarta EE로 변경 (오라클이 이클립스 재단으로 JAVA EE를 이관해서 명칭이 변경). <br/>
자카르타EE는 최신 기술 트렌드를 반영하고, 기존 JCP 정책이 아닌 JESP(오픈 소스 기반 자카르타EE 사양 프로세스) 라는 개방적이고 중립적인 정책을 따름. <br/>

- **GraalVM 기반 Spring Native 공식 지원**

- **HTTP/RSocket Interface Client를 제공**

- **Micrometer Observation API가 자동으로 구성, Observability 가 공식 지원을 시작**

- **HTTP API 에러 처리를 위한 RFC 7807 스펙을 지원합**

- 보안상 이슈로 /api/hello 와 /api/hello/ 는 더 이상 일치하지 않음

- Logback, Log4j2의 날짜 및 시간의 기본값이 ISO-8601 표준을 따름




<br/></br>

**Java EE(Java Platform, Enterprise Edition)**

특정 운영체제와 미들웨어에 종속되지 않고 정보 교환 및 애플리케이션 호환이 가능한 플랫폼을 제공

자바EE는 1999년 썬 마이크로시스템즈가 J2EE(Java 2 Enterprise Edition) 명으로 발표한 분산 애플리케이션 개발 목적의 산업 표준 플랫폼

기업용 애플리케이션을 개발/실행하기 위한 기술과 환경을 제공하며 서블릿(Servlet), JSP, EJB, JDBC, JNDI, JMX, JTA 등의 알려진 기술을 포함한다. 

오라클이 이클립스 재단으로 JAVA EE를 이관했다. 자카르타EE는 자바EE를 대체하지 않았고 둘 다 공존하고 있는 상태

<br/></br>
**Spring Native**

자바 및 코틀린을 지원하며 독립실행파일로 배포/실행 가능하다! (JVM 설치가 필요없다)

GraalVM를 활용하여 네이티브 이미지로 컴파일하여 JVM에 비해 빠른 빌드, 빠른 어플리케이션 시작시간, 적은 메모리를 사용

- GraalVM
  - 자바로 만들어진 새로운 JIT 컴파일러
  - Oracle이 만든 JVM과 JDK으로 애플리케이션 성능과 효율성의 향상을 제공하는 고성능 런타임
  - https://velog.io/@akfls221/Spring-GraalVM-Native-Image




