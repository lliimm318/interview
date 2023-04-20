# NULL

Null... 개발하면서 누구나 만났고,,, 만나면 아주 짜증나고 아주 중요한 친구이다.<br/>
NULL은 상수이며 0, ""이 아닌 **아무 것도 없음**을 의미한다. 

NULL 만든 영국의 컴퓨터 과학자인 Tony Hoares는 NULL 포인터를 10억달러짜리 실수라고 말하기도 했다.


## null을 왜 싫어하시나

**에러 핸들링**

객체 null 체크가 필요하다. (안하면 NPE 빵!)<br/>
그래서 코드에 예외처리가 필요하다. (try / catch / throw exc exception... 등등)

처음부터 null이 아닌 객체가 확실하다면 위의 과정은 안해도 된다 -> 불필요한 코드가 생긴다.
<br/><br>

**의미가 모호하다**

사용자 정보를 가저오는 getUserInfo() 함수가 있을 때, 의미를 명확하게 하려면 getUserInfoOrNullIfNotFound() 이렇게 정의해야 한다. 그치만 이렇게 된다면 함수 이름은 길어지고.. 
모호성을 없애뎌면 실제 객체나 null 또는 exception을 넘겨야한다.





참고) https://zorba91.tistory.com/339
