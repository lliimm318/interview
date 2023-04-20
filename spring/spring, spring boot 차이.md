# spring, spring boot 차이

스프링과 스프링 부트의 차이를 나한테 묻는다면 잘 말할 수 있을까?

일단 나는 아니다.. 스프링 보다 제공해주면 스프링 부트.. 딱 이 정도 까지의 수준밖에 말을 하지 못한다.

## Spring이란?

정확히는 스프링 프레임 워크이다!

나는 


## 차이점!

### dependency
**Spring** - 매우 길며, 모든 dependency를 버전까지 지정해야함

**Spring boot** - Spring에 비해 매우 짧아졌으며, 버전 관리도 권장 버전으로 자동 설정해준다!

~~~
spring boot-starter-data-jpa
spring boot-starter-security
spring boot-starter-test
spring boot-starter-web
~~~
위와 같은 spring boot-starter 가 들어간 친구들을 사용하면, 의존성이 걸린 친구들을 알아서 가져와 준다!

### Configuration
**Spring** - 매우 길다.. 빈을 어떻게 할지 등등 넘 많고 관리해야할게 너무너무 많다

**Spring boot** - application.properties or application.yml 사용하면 훠얼ㅅ어씬 짧고 간단하게 사용 가능하다. ( 난 yml파이다.. ㅎ 더욱 휴먼어블한 느낌
<br/><br>
### 내장 서버

**Spring** - 내장 서버가 없어서 외부에서 가져와서 하나하나 설정 하고 띄우고.. 시간이 오래 걸린다.

**Spring boot** 
- 서버 구동 시간이 절반 가까이 단축된다! 톰캣이가 안에 살고 있다. 이 야옹이가 싫으면 제티 등으로 간편하게 변경 가능하다
- 내장 서블릿 컨테이너 덕분에 **jar**로 간단하게 배포 가능하다!!!


### 우리 Spring boot는요..

개발자들이 개발에만 집중할 수 있도록 해줍니다!!!

1. 간편한 설정
2. 편리한 의존성 관리 & 자동 권장 버전 관리
3. 내장 서버가 있어 간단한 배포 서버 구축 가능
4. 다른 스프링 프레임 워크 요소(Data Jap, security 등)를 쉽게 사용 가능
