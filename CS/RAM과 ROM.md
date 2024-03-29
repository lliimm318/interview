# RAM과 ROM
*학동쌤이 무척이나 생각나는 주제...*

![image](https://user-images.githubusercontent.com/66578746/232631598-ae53b011-a542-43c7-8a82-002b139b0c04.png)
이 친구들도 종류가 많아요

## RAM (주기억장치)
- 자유롭게 읽고 쓸 수 있는 기억장치이다. 현재 사용중인 프로그램이나 데이터가 저장되어 있다.
- 휘발성이다. (시스템 전원이 꺼지면 저장된 내용이 사라짐!)

임의 엑세스 메모리이다. CPU가 RAM 메모리의 모든 주소 위치에 직접 접근 가능하다!
RAM은 컴퓨터에서 빠르게 접근 할 수 있는 메모이리며, **일시적으로** 데이터를 저장한다.

휘발성 메모리로 RAM은 전원이 꺼지기 전까지 데이터를 저장한다.
현재 처리 해야하는 데이터는 RAM에 있는다.

컴퓨터에서 가장 빠르고 비용이 많이 드는 메모리다.
읽기 쓰기 메모리여서 RAM에서 명령어를 읽고 결과를 RAM에 쓸 수 있다.
**데이터를 수정할 수 있다!**

정적RAM(SRAM)과 동적RAM(DRAM)이 있는데, SRAM은 내부 데이터를 유지하기 위해 지속적인 전력 흐름이 필요하다.
DRAM보다 빠르지만 비싸다.. 주로 컴퓨터의 **캐시 메모리**로 쓴다

DRAM은 보유한 데이터를 유지하려면 새로고침 해야한다. SRAM 보다는 느리지만 싸당

## ROM 
- 기억된 내용을 읽을 수만 있다. (쓰기 불가능!!)
- 비휘발성 메모리이다. (전원이 꺼져도 저장된 내용이 사라지지 않음!)
그래서 변경 가능 성이 없는 시스템 소프트웨어를 기억시키는데 이용한다!

읽기 전용 메모리라서 CPU에서 읽을 수는 있지만 수정이 불가하다.
CPU가 ROM 메모리에 직접 접근할 수 없으면 데이터를 RAM으로 먼저 전송한 다음 CPU가 RAM에서 해당 데이터에 접근할 수 있어야한다.

부트 스트랩하는 동안 컴퓨터가 필요로 하는 명령(컴퓨터 부팅)을 저장한다.
ROM의 내용은 수정할 수 없다. 비휘발성 메모리라서 CPU의 전원이 꺼져도 ROM 내부의 데이터는 유지된다.

ROM은 RAM보다 용량은 비교적 작고, 속도는

**ROM의 종류**
PROM - 프로그래머블 ROM. 사용자가 한 번만 수정 가능함!
EPROM - 지우고 프로그래밍이 가능한 ROM이다. 이 롬의 내용은 자외선을 사용하여 지울 수 있으며 ROM은 다시 프로그래밍 가능하다.

## 프로그램 실행순서
![image](https://user-images.githubusercontent.com/66578746/232631688-6603a58a-9096-4a3d-8aba-31f72ca50ccb.png)

1. 사용자가 프로그램 실행을 요청한다.
2. OS가 프로그램 정보를 읽어 메모리에 로드되고
3. 프로그램이 실행되면 OS는 메모리(RAM)에 공간을 할당한다
4. CPU는 기계어 코드를 실행한다.


### 참고

부트스트랩이란? - https://m.blog.naver.com/dlaxodud2388/222105963737

RAM과 ROM -  https://code4human.tistory.com/129#:~:text=RAM%EC%9D%98%20Data%20%EC%98%81%EC%97%AD%EC%97%90%EB%8A%94,%EC%9D%B4%20%EC%A2%85%EB%A3%8C%EB%90%98%EB%A9%B4%20%EC%86%8C%EB%A9%B8%ED%95%9C%EB%8B%A4
