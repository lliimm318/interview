# Optional
NPE를 피하려면 null 체크를 해야하는데 (초기값 지정도 좋다), Optional<> 클래스는 NPE를 방지하게 한다. 

**Optional<T>는 null이 올 수 있는 값을 감싸는 Wrapper 클래스이다!**
<br/><br>  
## 사용해 보아요
### 데이터가 null일 때

``` java 
public final class Optional<T> {

  private static final Optional<?> EMPTY = new Optional<>();
  private final T value;
    
  private Optional() {
     this.value = null;
  }

  (생략)

}
```
**Optioanl.empty()**
 
Optional 클래스 안에 static 변수로 EMPTY 객체를 생성해 놨다. 그래서 EMPTY 객체를 공유하여 빈 객체를 여러번 생성하지 않아도 된다.
<br/><br>  
### 데이터가 절대 null 아닐 때
``` java
Optional<String> string = Optional.of("문자열");
```
**Optional.of()**

데이터가 절대 null이 아니라면 Optional.of를 통해 생성할 수 있다. 만약 Optional.of로 저장하려는 데이터가 null이면 NPE 뜬당 ㅎ
<br/><br>  
### 데이터가가 null일 수도 있고 아닐 수도 있을 때
``` java
Optional<String> string = Optional.ofNullable(getStr());
String str = optioanl.orElse("not found");
```
**Optional.ofNullable()**

null일 수도 있고 아닐 수도 있는 경우에 Optioanl.ofNullable()로 생성할 수 있고,<br/>
이후에 **orElse** / **orElseGet**을 통해 null인 경우에도 안전하게 값을 가져올 수 있다.
<br/><br>  

## orElse orElseGet 차이
orElse는 값을 생성해서 orElseGet보다 비용이 크다.

orElse - 파라미터로 값을 받는다.<br/>
파리미터 값이 필요한 경우 or 값이 미리 존재하는 경우 사용

orElseGet - 파라미터로 함수형 인터페이스를 받는다.<br/>
함수가 필요한 경우 or 값이 미리 존재하지 않는 경우
ex) 회원 가입
<br/><br>

## Optioanl이 위험해요
아니 NPE도 피해주는 고마운 친구 아냐? 뭐가 위험하다고ㅡㅡ

맞다 Optiponal쓰면 Null-safe해지고 가독성도 좋고 안정적인 어플리케이션을 가질 수 있다. 과한건 독이 된다고,,, 사이드 이펙트가 생길 수 있다.
<br/><br>
### NoSuchElementException
NullPointException 말고?? 저건 뭐냐
``` java
Optional<User> optioanlUser = ;
User user = optionalUser.get() //optioanl이 갖는 값이 없너서 NoSuchElementException
```
이름에서 알 수 있듯 optional이 갖는 값이 존재하지 않으면 생기는 에러이다. 
<br/><br>
### 오버헤드
Optioanl은 객체를 감싸는 컨테이너 이다. 그래서 Optioanl 객체 자체 저장을 위한 메모리가 필요하고, Optioanl 안에 있는 객체를 접근해야 함으로 시간이 걸린다.

<br/><br>
## '잘'사용해 보아요
### Optioanl에 null 할당 금지
간혹 값이 없는 경우 optional에 null을 넣는 사람이 있다. 진짜 딱밤이다! Optioanl은 박싱 클래스이다. Optional에 null을 할당하는 짓은 다시 이 객체를 null체크 해야한다는 이야기다! 

값이 없는 경우면 **Optioanl.empty**를 사용하자!!!
<br/><br>
### 값이 없을 때, Optional.orElseGet() 로 기본값 반환
객체를 검사할 때, isPresent()로 검사하고 orElseGet()이용해서 가져와랑.
<br/><br>
### 생성자 수정자 메소드 파라미터에 Optional 넘기지 마!
optional은 변환 타입으로 사용해야한다.



<br/><br>    
참고)
 
https://mangkyu.tistory.com/70

https://mangkyu.tistory.com/203
  
