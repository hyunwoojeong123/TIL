## Minimum Spanning Tree

그래프 G의 spanning tree 중 edge weight 의 합이 최소인 `spanning tree`를 말한다.

`spanning tree`: 그래프 G의 모든 vertex가 cycle이 없이 연결된 형태를 말한다.

최소 신장 트리를 구하는 알고리즘은 크게 2가지 Kruskal, Prim Algorithm이 있다.



## Kruskal Algorithm

**시간복잡도**

1. Edge의 weight를 기준으로 sorting - O(E log E)
2. cycle 생성 여부를 검사하고 set-id를 통일 - O(E + V log V) => 전체 시간 복잡도 : O(E log E)



##### 구현 - BOJ 1197

```python
# edges를 가중치가 작은 게 앞에 오게 sort E*logE
# 싸이클 안생기게 유니온 파인드로 같은 부모인지 확인하면서 간다
# 다 연결댈 때까지만 한다

def find_set(x):
    if p[x] != x:
        p[x] = find_set(p[x])
    return p[x]

def union(x,y):
    p[find_set(x)] = find_set(y)

V,E = map(int,input().split())
edges = []
for _ in range(E):
    st,ed,w = map(int,input().split())
    edges.append([st,ed,w])
p = [x for x in range(V+1)]

edges = sorted(edges, key = lambda x : x[2])
cnt = 1
idx = 0
ans = 0

while cnt < V and idx < E:
    x,y,w = edges[idx]
    if find_set(x) != find_set(y):
        union(x,y)
        cnt += 1
        ans += w
    idx += 1
print(ans)

```



## Prim Algorithm

1) 한 개의 vertex 로 이뤄진 초기 그래프 A를 구성한다.

2) A 내부에 있는 vertex로부터 외부에 있는 vertex 사이의 edge를 연결하는데 그 중 가장 작은 weight 의 edge를 통해 연결되는 vertex를 추가한다. (어떤 vertex 건 간에 상관없이 edge의 weight를 기준으로 연결)

3) 위 과정을 반복하고 모든 vertex들이 연결되면 종료한다.



**시간복잡도**

=> 전체 시간 복잡도 : O(E log V)



##### 구현

1) 배열을 이용한 방식

```python
# 2) 배열 이용한 prim
# 1. 임의의 시작점 하나를 선택한다.
# 2. 이 시작점과 연결된 정점들의 거리를 업데이트 한다.
# 3. 선택된 정점들과 연결되어 있는 간선들 중에서, 가장 짧은 길이의 간선을 선택해서 연결해준다.
# 4. 가장 짧은 간선으로 연결되어 있는 정점을 선택하고, 정점들의 거리를 업데이트 한다.
# 5. 3 ~ 4 번의 과정을 N-1 번 만큼 반복해준다.
V,E = map(int,input().split())
linked = [[] for _ in range(V+1)]
Select = [False for _ in range(V+1)]
dist = [987654321 for _ in range(V+1)]
for _ in range(E):
    start,end,weight = map(int,input().split())
    linked[start].append([end,weight])
ans = 0
dist[1] = 0
Select[1] = True
for link in linked[1]:
    Next,Distance = link
    dist[Next] = Distance

for i in range(1,V):
    Min_Cost = 987654321
    Min_Idx = -1
    for j in range(1,V+1):    
        if Select[j]:
            continue
        if Min_Cost > dist[j]:
            Min_Cost = dist[j]
            Min_Idx = j
    Select[Min_Idx] = True
    ans += Min_Cost

    for link in linked[Min_Idx]:
        Next,Distance = link
        if Select[Next]:
            continue
        if dist[Next] > Distance:
            dist[Next] = Distance
print(ans)
```



2) pq를 이용한 방식 (배열보다 더 빠름)

```python
# 1) pq 이용한 prim
import heapq
V,E = map(int,input().split())
linked = [[] for _ in range(V+1)]
for _ in range(E):
    start,end,weight = map(int,input().split())
    linked[start].append([weight,end])
    linked[end].append([weight,start])

Select = [False for _ in range(V+1)]
pq = []
ans = 0
cnt = 1
for link in linked[1]:
    Distance,Next = link
    heapq.heappush(pq,[Distance,Next])
Select[1] = True
while pq:
    Distance,Cur = heapq.heappop(pq)
    if not Select[Cur]:
        Select[Cur] = True
        ans += Distance
        cnt += 1
        for link in linked[Cur]:
            nDistance,Next = link
            if not Select[Next]:
                heapq.heappush(pq,[nDistance,Next])
    if cnt == V:
        break

print(ans)
```



