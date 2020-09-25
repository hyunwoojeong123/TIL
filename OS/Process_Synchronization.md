# 프로세스 동기화

### Critical Section(임계영역)

여러 스레드가 동일한 자원에 동시 접근하는 경우 해당 영역을 Critical Section이라 한다.

### Critical Section Problem(임계영역 문제)

프로세스들이 Critical Section을 함께 사용할 수 있게 프로토콜을 설계하는 것

### Requirements

- Mutual Exclusion(상호 배제)

프로세스 P1이 Critical Section에서 실행 중이면 다른 프로세스들은 해당 Critical Section에서 실행 안됌.

- Progress(진행)

Critical Section 에서 실행중인 프로세스가 없고, 별도의 동작이 없는 프로세스들만 Critical Section에 진입후보가 될 수 잇다.

- Bounded Waiting(한정된 대기)

P1가 Critical Section 에 진입 신청 후부터 받아 들여질 때까지 다른 프로세스들이 Critical Section에 진입하는 횟수에 제한을 둔다.

### 방법

#### Lock

- 하드웨어 기반 해결책, Critical Section에 진입하는 프로세스는 Lock을 획득하고 Critical Section을 빠져나올 때 Lock을 방출해 동시에 임계영역 접근 안하게 한다.

#### 문제점

- 시간 효율성이 매우 떨어진다.



#### Semaphores(세마포)

##### 종류

- 카운팅

가용한 자원의 개수로 초기화,자원을 사용하면 세마포 감소, 방출 시 세마포 증가

- 이진(MUTEX)

상호배제, 0과 1사이 값만 가능. 다중 프로세스들 사이의 Critical Section 문제 해결 위해 사용

##### 단점

- Busy Waiting(바쁜 대기)

세마포 초기버전인 Spin lock에서 Critical Section에 진입해야 하는 프로세스는 진입 코드를 계속 반복 실행하며  CPU 시간을 낭비. 이를 Busy Waiting이라 했다.

##### ->해결책 : 일반적으로 Critical Section에 진입 시도했다 실패한 프로세스를 Block시킨 후 자리가 나면 다시 깨운다.

#### Deadlock(교착 상태)

- 세마포가 Ready Queue를 가지고 있고, 둘 이상의 프로세스가 Critical Section 진입을 계속 기다리고 있고, Critical Section 에서 실행되는 프로세스는 진입 대기 중인 프로세스가 실행되어야만 빠져 나올 수 있는 상황



#### Monitor(모니터)

- Critical Section 에 접근하기 위한 키 획득과 자원 사용 후 해제를 모두 처리 ( 세마포는 직접 키 해제와 Critical Section 접근 처리가 필요)