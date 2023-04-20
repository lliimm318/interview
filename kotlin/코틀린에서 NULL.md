내가 코틀린 코드를 너무 자바처럼 짜서 정리한다!

# 코틀린과 NULL
나는 NULL이 싫다. 꼴보기 싫다. 스트레스 받는다. NPE 너무 싫다!!!!

위에서의 찡찡이는 내가 코틀린 개발자는 아니라는 것을 증명한다.
<br/><br>
## Java에서 NULL
자바에서 null을 쓸 때,

API null 사용을 최대한 하지 마라, 초기화를 명확하게 해라, Optional을 사용해라 등등..

요런 말이 있다. 위는 null을 회피하게 만들거나, 많은 boilerplate코드를 만든다. 자바 개발자 입장에서 사용하면 좋지만, 솔직히 아쉽다..
<br/><br>
## 과연 null이 나쁠까?

null을 만든 토니 호어도 null은 10억 달러짜리 실수라매?<br/>
> ㄴㄴ 그건 널 포인터고

null을 가르키는게 실수지 null이 실수라곤 안했다! 

소프트웨어는 값이 없음을 나타낼 무언가가 필요하고, null은 값이 없음을 나타내는 가장 효율적인 방법이다! 따라서 null은 회피가 아닌, null의 의미를 살려 사용해야 한다!

자바에서 String = null 을 사용하면 에러가 난다. 이는 null 자체에 에러가 있는게 아니라 string에 null을 허용하는 자바 타입이 문제가 있다고 생각한다. 
그래서 나를 포함한 자바 개발자들이 null을 회피하도록 코드를 짜는게 아닐까? (나는 코틀린에서도 자바처럼 짜는 경향이 있다,,
<br/><br>
## 코틀린은 null 허용
``` kotlin
var str1: String = null // 컴파일 에러
var str2: String? = null // 컴파일 성공
str2.split(':')  // 컴파일 에러
str2?.split(':')  // 컴파일 성공
```

? 를 붙이면 null 할당 가능한 프로퍼티이다. 
<br/><br>
## 그러면 NPE가 없나욤?
아뇨 있답니다!

NPE가 없을거 같지만! 자바 라이브러리를 사용하면 발생해요.. 자바는 Non-NULL이 없어서 이를 Nullable로 칩니다. 

!! 연산자는 null이 아닌 것을 보장하기에 사용하면 좋아욤 (그치만 null이면 NPE 납니당)


참고) <br/>
https://wooooooak.github.io/kotlin/2020/10/27/kotliner%EB%8A%94_null%EC%9D%84_%EC%96%B4%EB%96%BB%EA%B2%8C_%EB%B0%94%EB%9D%BC%EB%B4%90%EC%95%BC_%ED%95%98%EB%8A%94%EA%B0%80/

