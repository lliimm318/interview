# RestTemplate / WebClient / Feign

다른 서버랑 통신하기 위해서 사용되는 친구들이에용

## RestTemplate

HTTP 요청을 만들기 위해 Spring Framework에서 제공하는 동기식 클라이언트 라이브러리! 파스토 입사에서 처음으로 본 친구이다.
오랫동안 사용하고 대규모 커뮤니티가 존재하는 안정적인 라이브러리 ~

주로 Spring MVC 기반에서 사용. JSON, XML 등 다양한 형식의 데이터를 처리 가능하다.

~~~ java
RestTemplate restTemplate = new RestTemplate();
String url = "https://api.example.com/users/{id}";
User user = restTemplate.getForObject(url, User.class, 1);
~~~
 
- 동기로 동작 -> 응답 받을 때까지 대기하며 스레드 차단한다. 대량의 요청 처리 시 성능 이슈가 발생한다
- Spring 5.0 이후부터 RestTemplate은 레거시 라이브러리로 간주해서 WebClient가 권장됨

## WebClient

spring5 부터 도입된 비동기식 HTTP 클라이언트 (동기로도 사용 가능)
Non-Blocking I/O 모델을 기반으로 하며, 비동기 및 리액티브 스트림 처리를 지원

~~~ java
WebClient webClient = WebClient.create();
String url = "https://api.example.com/users/{id}";
Mono<User> userMono = webClient.get()
        .uri(url, 1)
        .retrieve()
        .bodyToMono(User.class);
~~~

- 비동기 작업. 리액티브 타입인 Flux와 Mono를 반환하여 비동기 결과 처리에 좋다
- 대량의 요청 처리 성능과 확정성 면에서 좋다

  
