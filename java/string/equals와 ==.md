둘 다 양쪽에 있는 내용을 Boolean 값으로 반환한다는 공통점이 있다!

# 차이


## 형태가 다르다
equals()는 메소드고, ==은 비교를 위한 연산자이다.


## 비교 내용
equals는 비교하는 대상의 내용 자체를 비교한다. 하지만 ==은 대상의 주소값을 비교한다.

> String a = "aaa";  
> String b = a;<br/>
> String c = new String("aaa");<br/>

위에서 a와 b는 같은 주소 값이지만, c는 객체 생성을 통해 새로운 주소가 할당 된다.

> a.equals(b) // true 같은 내용을 비교 <br/>
> a == b // true 같은 주소값을 비교해서<br/>
> a == c // false 다른 주소값을 비교<br/>
> a.equals(c) //true 같은 내용을 비교

참고 > https://ojava.tistory.com/15
