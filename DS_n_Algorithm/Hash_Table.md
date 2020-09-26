# Hash_Table

> 배열을 사용해 값을 저장하므로 검색 시간이 O(1)로 매우 빠르다.
>
> 문제점은 이 인덱스로 저장되는 `key` 값이 불규칙하다.

-> 그래서 <b>특별한 알고리즘</b>을 사용해 저장할 데이터와 연관된 유일한 숫자를 만들어서 이를 인덱스로 사용한다.

특정 데이터가 저장되는 인덱스는 그 데이터만의 고유한 위치이기 떄문에, 삽입 ,삭제도 빠르게 가능하다. 



## Hash Function

> 위에서 언급한 <b>특별한 알고리즘</b>을 Hash Function 이라 한다.

이 함수를 잘 짜는 것이 중요하다. 왜냐하면, 1:1로 만들면 array와 똑같고 메모리를 너무 많이 먹는다. 따라서 충돌을 줄이는 방식으로 짜야한다. 충돌이 많아지면, 검색에 필요한 시간이 늘어나기 때문이다.



### 충돌을 해결하는 방법들

- Open Address

충돌 발생시 다른 곳에 데이터 삽입

1. Linear Probing 순차적으로 탐색해 비어있는 곳을 찾을 때까지 진행
2. Quadratic Probing 2차 함수를 이용해 탐색
3. Double Hashing Probing 하나의 해쉬 함수에서 충돌이 발생하면 2차 해쉬 함수를 이용해 새 주소를 할당.

- Separate Chaining

Open Address 보다 빠르다.

1. 연결 리스트 사용

각 바구니들을 연결리스트로 만들어서 충돌 발생시 해당 바구니의 list에 추가

2. Tree 사용(Red-black Tree)

연결 리스트 대신 Tree사용함. 데이터 많으면 트리, 적으면 연결 리스트

트리는 메모리 사용량이 연결리스트보다 많다.


