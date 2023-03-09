# JIT
언어를 번역하는 방법은
1. interpreter
기계어로 변환된 코드를 실행 파일로 작성하지 않고 메모리에 바로 로드 시켜 실행한다. 코드를 한줄씩 읽어 다른 중간 코드나 기계어로 임시 변환하고 변환한 것을 바로 실행한다.
장점 - 코드를 한줄씩 실행해서 에러 발생시 실시간 코드 수정 가능
단점 - 느린 실행속도, 변환과 실행을 동시에 진행해서 느림

2. compile
언어 (.c) -> 컴파일러가 목적파일로 변환 (.obj) -> 링커 실행파일 (.exe) -> 로더 -> 실행
장점 - 빠른 실행 속더
단점 - 한꺼번에 컴파일해서 컴파일 시간 큼. 운영체제별로 컴파일 해야한더. 수정 사항 발생시 다시 컴파일..

이렇게 두가지 방법이 있다. JIT compiler는 위에 두개를 쓴다.
<br/></br>
### 어떻게 그럴까????
JVM도 처음엔 인터프리터 방식으로 모든 바이트 코드를 실행한다. 그 중 자주 사용되는 메서드는 캐시에 컴파일된 바이너리 코드를 저장한다. 

interpreter (빠른 초기 실행 속도) 와 compile (실행 성능 )의 장점을 합쳤다. 
<br/></br>

## 동작방식
1. 실행할 때 컴파일 하면서 해당 코드를 캐싱
2. 그 이후에 바뀐 부분만 컴파일하고 캐싱된 코드 사용
3. JVM은 코드를 바로 컴파일 하지 않음 (한 번만 실행하면 인터프리터하는 편이 더 빨라서 컴파일러하기 충분한 코드를 찾는다)
 
#### 최적화 
컴파일러는 **메인 메모리에서 값을 사용할 시기**와 **레지스터 내의 값을 저장할 시기**를 결정한다.

``` java
public void calculateSum(int n) {
    for(int i = 0; i < n; i++) {
        sum += i;
    }
}
```
위와 같은 코드가 있을 때, sum 변수는 인스턴스 변수이다. 즉 메인 메모리 안에 있어하지만, for문이 반복될 때마다 sum 값을 메인에서 조회, 저장하면 성능은 좋지 않다. sum의 초기값을 레지스터로 로드하고 레지스터 내의 값을 이용해 for문을 수행한 다음 결과 값을 메인에 저장하는 최적화 방법을 사용할 수 있다.



## Compilation Level
JIT는 C1 (초기 실행 속도 중점), C2 (실행 중 성능) 컴파일로 이루어져 있다.<br/>

C1 - level1, 2, 3 세 단계 컴파일 레벨<br/>
> 가능한 빨리 코드를 최적화하고 컴파일에 최적화.
                      
C2 - level4 의 컴파일 레벨<br/>
> C1에 비해 더 오래 코드를 관찰 / 분석해서 더 나은 최적화<br/>
<br/></br>
Level0
- 모든 Java 코드를 Interpreter 방식으로 해석<br/>
#### C1<br/>
Level 1	<br/>
- 메소드를 프로파일링을 하지않고 컴파일. 메소드 복잡성이 낮기때문에 최적화가 필요한 부분이 업프로파일링을 통한 C2 컴파일이 의미가 없기 때문<br/>

Level 2<br/>
- C2 컴파일 큐가 가득 찼을때 최대한 빨리 컴파일 하기 위해 사용<br/>

Level 3<br/>
- 사소하고 간단한 메소드(Level 1)가 아니거나 C2 컴파일 큐가 가득찬 경우(Level 2)가 아닌 그 외의 모든 경우에 사용. 가장 일반적인 컴파일 단계 시나리오는 Level 0에서 Level 3로 점프한다.<br/>

#### C2<br/>
Level4
	





<br/></br>
참고) <br/>
- [JIT(Just In Time) 컴파일러 :: 으뜸별](https://beststar-1.tistory.com/3)<br/>
- https://nopainnocode.tistory.com/15