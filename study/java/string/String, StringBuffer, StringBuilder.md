# String
## String vs StringBuffer vs StringBuilder
1. 문자열의 가변과 불변
2. 연산에 따른 String 객체생성 여부
3. 멀티스레드 여부에 따른 동기화
4. 저장 위치

### 가변) String
> String은 불변 문자열이다. 즉 문자열이 할당된 **메모리 공간이 변하지 않는다**!

"+"로 문자열을 추가할 때, 새로운 문자열 객체가 생성되어 참조자는 새로운 문자열 객체를 참조하게 된다.
기존 문자열은 참조가의 참조가 사라져서 GC의 냠냠 대상이 된다. **== 연잔 자체가 객체 생성**
<br/></br>
장점 - 간단함, 스레드 세이프, 내부 데이터 공유가능.      
단점 - 문자열 연산이 많다면, 성능이 안좋아진다. (자원을 많이 사용해서 오버해드가 발생한다..)
<br/></br>

### 불변) StringBuffer, StringBuilder
> 둘은 가변 문자열이다. 즉 문자열이 할당된 **메모리 공간이 변한다**<br/>

.append()로 **동일한 객체**의 문자열을 추가하면 추가된 문자열에 따라 크기를 변경하면서 문자열을 변경한다.
최종적으로 .toString()으로 객체를 한번만 생성한 문자열을 만든다.
<br/></br>
장점 - 문자열 연산이 많은 경우 우수한 성능.    
단점 - read의 경우 새로운 String을 생성해서 성능이 떨어진다.
<br/></br>

### StringBuffer vs StringBuilder
> 동기화의 유무 차이!

**String Buffer**<br/>
동기화를 지원 -> 멀티스레드 환경에 적합.  
안에 synchronized 키워드가 선언되어 있다

**String Builder** - 동기화를 지원하지 않는다 -> 싱글스레드, 멀티스레드지만 동기화가 필요없을때.   
String Builder가 동기화를 고려하지 않아서 싱글스레드 환경에서 연산처리가 빠르다!
<br/></br>

### 저장위치
> new로 생성한 String은 Constant Pool에 저장, 나머지는 Heap에 저장 

Constant Pool (상수풀)이란 Integer, String과 같은 레퍼런스 타입의 데이터 값, 메소드 호출, Class 호출 등을 저장하는 JVM 메모리 공간이다 <br/>
Heap 영역은 new로 셍성한 객체가 저장된다. 


참고 > https://starkying.tistory.com/entry/what-is-java-string-pool
