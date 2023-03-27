# spring batch
spring batch는 엔터프라이즈 시스템 운영에서 **대용량 일괄처리** 편의를 위해 설계된 가볍고 포괄적인 배치 프레임워크이다.

### 배치란?
배치 작업은 실시간으로 데이터를 처리하는게 아니라 일괄적으로 모아서 처리하는 작업을 의미한다.

특징
- 대량의 데이터 처리
- 특정시간에 실행
- 일괄 처리

## spring batch
배치가 실패하여 작업을 재시작하면 실패한 시점부터 실행하며 중복 실행을 막기 위해 성공 이력이 있는 배치는 동일한 파라미터로 실행 시 에러가 난다.
### 용어

**Job** <br/>
배치처리 과정을 한 단위로 만든 객체이며 배치 과정에서 최상단에 있다.

**JobInstance** <br/>
job의 실행 단위이다. job을 실행 시키면 하나의 jobinstance가 생성된다.
1월1일, 1월2일에 실행을 하면 각각 jobinstance가 생성되는데 이 때 1월1일에 실행한 jobinstance가 실패해서 다시 실행을 시켜도 jobinstance는 1월1일 데이터만 처리한다.

**JobParameters**<br/><br>
joninstance의 실행 단위이다.

**JobExecution** <br/>
jobinstance에 대한 실행 시도에 대한 객체이다. jobinstance에 실행 상태, 시작 시간, 종료 시간, 생성 시간 등의 정보를 가지고 있다.
jobinstance가 실패해서 재실행을 하면 동일한 jobinstance를 실행하지만, jobexecution은 두번의 실행 각각 생성된다. 


