# volatile
자바 동시성 이슈를 해결하기 위한 방법 중 하나이다.

- 자바 변수를 메인 메모리에 저장
  - 변수의 값을 읽을 때마다 CPU 캐시에 저장된 값이 아닌 메인 메모리에서 읽음
  - 변수를 Write할 때마다 메인 메모리에 저장
 
<br/> 

-----

![image](https://github.com/lliimm318/interview/assets/66578746/6a7c4ff2-6a90-4e6b-af96-c8aaf6741747)

멀티스레드 환경에서는 성능 형상을 위해 메인 메모리에서 읽은 변수 값을 CPU 캐시에 저장한다.
스레드가 변수 값을 읽어올 때 각각의 CPU 캐시에 저장된 값이 달라서 **변수 값 불일치** 문제가 발생한다 !

### ex) public int counter = 0;

![image](https://github.com/lliimm318/interview/assets/66578746/3cdfadb5-6011-47cf-9e5d-e6c9563d9380)

상황)
- 스레드1은 counter 값을 더하고 읽는 연산을 한다. (Read & Write)
- 스레드2는 counter 값을 읽는 연산만 한다. (Read Only)

스레드1은 값을 카운터 값을 7로 증가시키고 있지만, 캐시에만 반영하고 메인 메모리에 반영되지 않는다. 그래서 스레드2는 카운터 값을 더하기 전인 0을 가져온다.

**volatile 를 사용하면 메인 메모리에 저장하고 읽어와서 변수 값 불일치 문제를 해결할 수 있다 !**
- 멀티 스레드 환경에서 하나의 스레드만 Read & Write 하고 나머지 스레드가 read 하는 상황에서 사장 최신의 값을 보장한다

### 주의점 !
![image](https://github.com/lliimm318/interview/assets/66578746/20a1a7b0-7cd3-42fb-89f5-26143f898dd5)

상황)
- 스레드1이 값을 읽어와서 1을 더하는 연산 (추가하는 연산을 실행했지만 아직 메인 메모리 반영 전)
- 스레드2가 값을 읽어서 1을 더하는 연산 (추가하는 연산을 실행했지만 아직 메인 메모리 반영 전)

두개의 스레드가 1을 추가하는 연산을 진행해서 결과가 2가 나와야하지만 각각 결과를 메인 메모리에 반영하여 결과가 1이 나온다.

하나의 스레드가 아닌 여러 스레드가 write하는 경우에는 적합하지 않다.
-> 그런데 하나의 스레드에서만 write 하더라도 그 변수에 대한 접근과 수정이 잦다면 다른 스레드에서 읽어올 때 원자성이 보장되지 않을 수도..

캐시보다 메인 메모리가 비용이 더 크기 때문에 성능에 어느정도 영향을 줄 수 있다.

<br/> 

[블로그](https://nesoy.github.io/articles/2018-06/Java-volatile)
