# Open Fegin

- 넷플릭스에서 처음 만들어진 HTTP client 도구이다. (외부 API호출을 쉽게하도록 도움)
- Feign 을 사용하면 웹 서비스 클라이언트를 보다 쉽게 작성가능하다.
- 여기서 선언적인 == 어노테이션인데, Open Fegin은 인터페이스에 어노테이션만 붙여서 구현 가능하다. (JPA 처럼!


``` java
@FeignClient(name = "OpenFeign", url = "${api.uri}")
public interface ExchangeRateOpenFeign {

    @GetMapping
    ExchangeRateResponse call(
            @RequestHeader String apiKey,
            @RequestParam Currency source,
            @RequestParam Currency currencies);

}
```

### 장점
- **인터페이스와 어노테이션 기반으로 작성할 코드가 줄음**
  > open feign을 사용했을 때, RestTemplate과 비교하여 작성할 코드가 상당히 적어서 생산성이 높아진다.

- spring MVC 어노테이션으로 개발 가능
- 다른 spring cloud 기술들과 통합이 쉬움

### 단점
- 기본 HTTP Client가 HTTP2를 지원하지 않는다... (HTTP Client 추가 설정 필요)
- 공식적으로 Reactive 모델을 지원하지 않는다.
- 경우에 따라서 애플리케이션이 뜰 대 초기화 에러가 발생할 수 있다 (Object Provider로 대응 필요
- 테스트 도구를 제공하지 않는다 (별도의 설정 파일을 작성하여 대응 필요



