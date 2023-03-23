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



<br/><br>    
참고) https://mangkyu.tistory.com/70
  
