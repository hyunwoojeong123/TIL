## Minimum Spanning Tree

그래프 G의 spanning tree 중 edge weight 의 합이 최소인 `spanning tree`를 말한다.

`spanning tree`: 그래프 G의 모든 vertex가 cycle이 없이 연결된 형태를 말한다.

최소 신장 트리를 구하는 알고리즘은 크게 2가지 Kruksal, Prim Algorithm이 있다.



## Kruskal Algorithm

1) edge 없이 vertex 들만으로 그래프를 구성한다.

2) weight가 제일 작은 edge부터 검토한다.

3) 그렇게 하기 위해 Edge Set을 non-decreasing 으로 sorting 해야 한다.

4) 가장 작은 weight에 해당하는 edge를 추가하는데 추가할 때 그래프에 cycle이 생기지 않는 경우에만 추가한다.

5-1) spanning tree가 완성되면 모든 vertex들이 연결된 상태로 종료가 된다.

5-2) 완성될 수 없는 그래프에 대해서는 모든 edge에 대해 판단이 이루어지면 종료



**어떻게 cycle 생성 여부를 판단하는가?**

Graph의 각 vertex에 `set-id`를 부여한다. 초기화 과정에서 각각의 vertex들을 1~n까지 값으로 초기화한다.

0은 어떠한 edge와도 연결되지 않았음을 의미하게 된다. 그리고 연결할 때마다 `set-id`를 하나로 통일시키는데, 값이 동일한 `set-id`가 많은 `set-id`값으로 통일시킨다.



**시간복잡도**

1. Edge의 weight를 기준으로 sorting - O(E log E)
2. cycle 생성 여부를 검사하고 set-id를 통일 - O(E + V log V) => 전체 시간 복잡도 : O(E log E)



##### 구현 - BOJ 1197

```python
# Union-FInd
class DisjointSet:
    def __init__(self,n):
        self.data = [-1 for _ in range(n)]
        self.size = n
        
    def upward(self, change_list, index):
        value = self.data[index]
        if value < 0:
            return index
        
        change_list.append(index)
        return self.upward(change_list, value)
    
    def find(self, index):
        change_list = []
        result = self.upward(change_list, index)
        
        for i in change_list:
            self.data[i] = result
            
        return result
    
    def union(self, x, y):
        x = self.find(x)
        y = self.find(y)
        
        if x == y:
            return
        
        if self.data[x] < self.data[y]:
            self.data[y] = x
        elif self.data[x] > self.data[y]:
            self.data[x] = y
        else:
            self.data[x] -= 1
            self.data[y] = x
            
        self.size -= 1

# Kruskal
V,E = map(int,input().split())
#linked = [[1000001 for j in range(V+1)] for i in range(V+1)]
edges = []
for _ in range(E):
    edges.append(list(map(int,input().split())))
# print(edges)
edges= sorted(edges,key =lambda x:x[2])
# print(edges)
set_id = DisjointSet(V+1)
ans = 0
for edge in edges:
    start,end,weight = edge
    if set_id.find(start) == set_id.find(end):
        continue
    else:
        ans += weight
        set_id.union(start,end)
    if set_id.size == 2:
        break
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



** 10.19 월욜에 다시 해보자.