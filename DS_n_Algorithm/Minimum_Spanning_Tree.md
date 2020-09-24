# Minimum Spanning Tree

> 그래프의 `spanning tree` 중 edge weight의 합이 최소인 `spanning tree`
>
> `spanning tree`: 그래프의 모든 vertex가 cycle이 없이 연결된 형태



## Kruksal Algorithm

1) edge 없이 vertex 들만으로 그래프를 구성

2) edge들을 오름차순으로 정렬

3) 가장 작은 weight에 해당하는 edge를 추가하는데 추가할 때 그래프에 cycle이 생기지 않는 경우에만 추가

4) `spanning tree`가 완성되면 모든 vertex들이 연결된 상태로 종료,

완성될 수 없는 그래프에 대해서는 모든 edge돌면 종료

#### 어떻게 cycle 여부 판단?

1) 각 vertex에 `set-id`를 부여

2) 초기화 과정서 모두 1~n 까지의 값으로 각각의 vertex들을 초기화 0: 어떤 edge와도 연결 안댐

3) 연결할 때마다 set-id를 하나로 통일, 값이 동일한 `set-id` 개수가 많은 `set-id`값으로 통일

> 굳이 이렇게 안하고 DFS같은거 돌려서 확인해도 될듯. 방문한 데 또 방문하면 나오게



#### 시간 복잡도 : O(E log E) (E: 엣지 개수)



## Prim Algorithm

1) 한 개의 vertex로 이루어진 초기 그래프 A를 구성.

2) A 내부의 vertex로부터 외부에 있는 vertex 사이의 edge를 연결하는데 그 중 가장 작은 weight의 edge를 통해 연결되는 vertex를 추가

3) 위 과정을 반복하고 모든 vertex들이 연결되면 종료



#### 시간 복잡도: O(E log V) (V: Vertex 개수)



** prim,kruksal로 문제 풀어보고 어떤 식으로 하는지 정리해서 올리자 **