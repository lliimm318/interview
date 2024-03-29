# 왜 GET은 바디를 안쓸까?

우리는 서버 개발을하면서 GET이라는 매소드를 자주 사용할 것이다.

GET은 RESTful API를 설계함에 있어서 자원을 조회는 용도로 쓴다. 
때문에 여기에 추가되는 API 파라미터들은 조회 조건을 설정하기 위해 사용함으로 보통 Path Parameter나 Query Parameter를 사용한다.

## 사용할 수 없는 경우
GET과 Body 사용은 사용할 수도 있고 못할 수도 있다.

### 1. 캐싱, 프록시

캐싱이나 프록시 설계 중 일부는 GET 의 body 값을 참조하지 않을 수 있다. 
그래서 body에 쿼리 조건을 넣는 경우 문제가 생길 수 있다..

### 2. RESTful Semantics
Semantics은 다른 구성원들이 이게 디자인된 철학으로 구현 됐겠지 하는 기대이다.
통용되는 의미론을 무시하면 시스템 설계가...

### 3. 지원하지 않는 경우
자프 때, 어쩔 수 없이 GET + BODY 조합을 사용해야만 하는 경우가 생겼는데, iOS는 GET Body를 지원하지 않는다..
추가로 spring rest template 경우에도 get 메소드를 사용하는 경우 바디 값을 보내지 않는다.

이처럼 특정 클라이언트나 서버는 GET의 BODY가 무시되는 경우가 있다.


## 그럼 안쓰나요?

URL로 표현불가한 복잡한 조회조건을 가진 경우에는 바디를 어쩔 수 없이 사용한다.

엘라스틱서치를 포함한 다양한 어플리케이션에서 GET + BODY 조합을 포함하는 경우를 종종 볼 수 있다.

상황에 따른 선택적으로 body를 사용해야한다.

<br/></br>
# 왜 안쓰나요!!

솔직히 이게 젤 중요하다고 생각한다. 개발자한테는 **왜?** 가 제일 중요하니까.

그동안은 그냥 아 GET BODY 같이 쓰면 안돼!라고 생각했지만 그게 왜 안되는지 정확하게 몰랐다.

## 탄생이유
GET은 리소스 검색을 위해 설계되었다.

- GET Method라도 body로 전송을 받을 수 없는 것은 아니다
- **서버로 데이터를 보내기 위해 사용되지 않는다.**
- HTTP GET 요청은 URL에 query parameters를 포함할 수 있지만, message body를 포함하는것을 권장하지 않는다.

<br/></br>
## GET Method 특징
- GET 요청을 캐시할 수 있습니다.
- GET 요청은 브라우저 기록에 남아 있습니다.
- GET 요청을 북마크할 수 있습니다.
- GET 요청은 민감한 데이터를 처리할 때 사용해서는 안 됩니다.
- GET 요청에는 길이 제한이 있습니다.
- GET 요청은 데이터를 요청하는 데만 사용됩니다(수정 아님).

<br/></br>
## 바디를 사용하지 않도록 권장하는 이유

1. 캐시 가능성

HTTP GET 요청은 종종 웹 브라우저에 의해 캐시된다. 
GET 요청을 간단하고 예측 가능하게 유지함으로써, 이러한 시스템이 캐시를 보다 쉽게 관리하고 검색할 수 있다.

2. 안전성

GET 요청은 "안전(safe)" 및 "멱등(idempotent)"이어야 한다.
이것은 서버에서 어떠한 데이터도 수정하지 않고 부작용이 없어야 함을 의미한다. GET 요청에서 메시지 바디를 허용하지 않음으로써, GET 요청이 안전하고 멱등하게 유지되도록 보장

3. 보안성 

GET 요청은 종종 서버 로그, 브라우저 히스토리 및 다른 시스템에서 기록된다. 
데이터를 URL에 유지함으로써, 이를 쉽게 볼 수 있으며, 제3자가 잠재적으로 가로챌 수 있다. 
반면, 메시지 바디에 데이터를 포함하는 POST 요청은 덜 가시적이며, 추가적인 보안 계층을 제공할 수 있습니다.
<br/></br>
### -> **HTTP 명세서에서 GET 요청에서 메시지 바디를 사용하지 않는 것은 캐시 및 보안 문제를 일으킬 수 있기 때문**


