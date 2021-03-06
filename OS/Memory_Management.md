# 메모리 관리 전략

> 각각의 프로세스는 독립된 메모리 공간을 갖고, OS 혹은 다른 프로세스의 메모리 공간에 접근 할 수 없다.
>
> OS 만이 OS메모리 영역, 사용자 메모리 영역에 접근 가능하다.



### Swapping

CPU 할당 시간이 끝난 프로세스의 메모리를 보조 기억장치로 내보내고(Swap) 다른 프로세스의 메모리를 부를 수 있다.



### Fragmentation

프로세스들이 메모리에 적재되고 제거되는일이 반복되면, 프로세스들이 사용하는 메모리 틈에 짜잘한 빈 공간이 많아진다.

- 외부 단편화 : 메모리 공간 중 사용하지 못하게 되는 일부분, RAM에서 사이사이 남은 공간들이 분산되어 있을 때 발생
- 내부 단편화: 프로세스가 사용하는 메모리 공간에 포함된 남는 부분. 프로세스에 10000B 할당하고 해당 프로세스가 9000B 사용하면 1000B가 남는데 이를 내부 단편화라 함

##### ->해결책: 압축 . 프로세스가 사용하는 공간을 한쪽으로 몰아 자유공간을 확보하는 것. 작업 효율이 좋지 않다.



### Paging

외부 단편화와 압축 작업의 문제점을 해소하기 위해 만들어짐.

물리 메모리는 Frame이라는 고정 크기로 분리, 논리 메모리(프로세스가 점유하는)는 고정 크기의 블록으로 분리.

프레임과 페이지는 똑같은 크기

페이징 기법 사용함으로써 논리 메모리가 물리 메모리에 저장될 때, 연속되어 저장하지 않고 남는 프레임에 적절히 배치한다.

하나의 프로세스가 사용하는 공간은 여러 개의 페이지로 나뉘고, 개별 페이지는 물리 메모리의 Frame에 맵핑된다.

##### ->단점: 내부 단편화 심해짐. ex) 페이지 크기 1000B 프로세스 A가 3172B 요구하면, 총 4개의 페이지 필요한데, 4번째 페이지는 900B정도 큰 공간이 놀게 된다.



### Segmentation

논리 메모리와 물리 메모리를 서로 다른 크기의 논리적 단위인 Segment로 분할.

사용자가 두개의 주소로 지정(Segment 번호 + 변위). 세그먼트 테이블에는 각 세그먼트의 시작 물리주소와 길이를 저장

##### ->단점: 서로 다른 크기의 Segment들이 메모리에 적재되고 제거되다 보면, 외부 단편화 심해짐

