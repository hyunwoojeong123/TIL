# Scheduler

>  3가지 큐를 사용한다.

- Job Queue : 현재 시스템 내에 있는 모든 프로세스의 집합
- Ready Queue : 현재 메모리 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 프로세스들
- Device Queue: Device I/O 작업을 대기하고 있는 프로세스의 집합



>  스케쥴러 종류도 3가지이다.

### 장기 스케쥴러 (Long-term scheduler or Job scheduler)

메모리는 한정되어 있는데, 갑자기 많은 프로세스들이 메모리에 올라오면, 대용량 메모리에 임시적으로 저장한다.

이 중에 어떤 애들을 메모리를 할당해 Ready Queue로 보낼지 결정한다.

- 메모리와 디스크 사이 스케쥴링 담당
- 프로세스에 각종 자원 할당
- 실행 중인 프로세스의 수 제어
- 프로세스의 상태 new -> ready

* TSS에서는 장기 스케쥴러 없음. 바로 메모리로 가서 ready 상태 된다.



### 단기 스케쥴러 (Short-term scheduler or CPU scheduler)

- CPU와 메모리 사이 스케쥴링 담당
- Ready Queue에 있는 프로세스들 어떤 프로세스를 실행시킬지 결정
- 프로세스에 CPU 할당
- 프로세스의 상태 ready -> running -> waiting -> ready



### 중기 스케쥴러 (Medium-term scheduler or Swapper)

- 여유 공간 마련을 위해 프로세스를 메모리에서 디스크로 쫓아냄 (swapping)
- degree of Multiprogramming 제어
- 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가지 못하게 한다.
- 프로세스의 상태 ready -> suspended



> Process state - suspended

프로세스 수행이 정지된 상태로 메모리에서 내려간 상태. 얘는 스스로 ready로 돌아갈 수가 없다. 감옥에 갔다.



### CPU 스케쥴러가 스케쥴 짜는 방식들



#### FCFS(First Come First Served)

- 먼저 온 애들을 먼저 처리
- 비선점형(Non-Preemptive) 스케쥴링

일단 CPU 한번 잡으면 완료될 때까지 반환 안한다.

- convoy effect : 소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상 발생

#### SJF(Shortest - Job - First)

- 다른 프로세스가 먼저 도착해도 CPU burst time이 짧은 프로세스에게 CPU를 먼저 할당
- 비선점형 스케쥴링
- Starvation : 사용시간이 긴 프로세스는 거의 영원히 CPU를 못 받고 굶어 죽는다.

#### SRT(Shortest Remaining Time First)

- 우선 순위가 가장 높은 프로세스에 CPU 할당
- 선점형 스케쥴링 방식 : 더 높은 우선순위 프로세스가 오면 실행중인 애 멈추고 CPU 준다.
- 비선점형 방식 : 더 높은 우선순위의 프로세스가 오면 Ready Queue의 맨 처음에 넣는다.

- Starvation
- 무기한 봉쇄(Indefinite blocking) : 실행 준비는 되어 있으나 CPU를 사용 못하는(우선순위 낮은) 프로세스가 계속 대기하는 상태

##### -> 해결책 : aging 오래 기다리면 우선순위 높여준다.

#### Round Robin

- 현대적임
- 각 프로세스는 동일한 크기의 할당시간(time quantum)을 가짐
- 할당 시간 지나면 CPU 뺏기고 ready queue의 맨 뒤로 간다.
- CPU 사용시간이 랜덤한 프로세스들이 섞여있으면 효율적
- 프로세스의 context를 저장해 context switch할 수 있어 가능
- Response time 빨라짐

n개의 프로세스 가 ready q에 있고 할당시간이 q인 경우 어떤 프로세스도 (n-1)q 이상 기다리지 않는다.

##### 주의점: 설정한 time quantum이 너무 커지면 FCFS와 같다. 너무 작으면 context switch를 너무 많이해  overhead가 발생. 즉, 적절한 `time quantum` 을 설정하는 것이 중요하다.

