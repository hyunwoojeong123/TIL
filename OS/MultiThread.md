# Multi Thread

> 하나의 프로세스를 다수의 스레드로 구분해 자원을 공유하고 수행 능력을 향상시킨다.

### 장점

- 분업을 통해 메모리 공간과 시스템 자원 소모를 줄인다. 

- Heap영역을 이용해 별도의 자원 안쓰고 스레드 간 데이터를 주고 받을 수 있다.
- 시스템의 Throughput이 향상되고 자원소모가 줄어 프로그램의 응답 시간이 단축된다.



### 문제점

- 스레드끼리 데이터와 힙 영역을 공유하기 때문에 한 스레드가 다른 스레드가 사용중인 데이터에 접근해 수정하거나 하는 문제가 발생할 수 있다.

##### -> 해결방법

동기화 작업이 필요하다. 동기화를 통해 작업처리 순서를 조절하고 공유 자원에 대한 접근을 조정한다.

하지만 이로 인해 병목현상이 발생해 성능이 저하될 가능성이 있다.



### 멀티 스레드 vs 멀티 프로세스

1. 멀티 스레드: 멀티 프로세스보다 적은 메모리 공간, 문맥전환이 빠르다. 오류로 인해 하나의 스레드가 종료되면 전체 스레드가 종료될 수도 있고, 동기화 문제가 있다.
2. 멀티 프로세스 : 하나의 프로세스가 죽어도 다른 애들에 영향을 안 미친다. 멀티 스레드보다 많은 메모리 공간,CPU 시간을 차지한다. 

> 적용하는 시스템에 따라 2개 중 잘 골라야 한다.