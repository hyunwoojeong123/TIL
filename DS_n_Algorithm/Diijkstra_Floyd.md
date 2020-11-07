# 다익스트라

특정한 하나의 정점에서 다른 모든 정점으로 가는 최단경로를 구한다.



### 작동 과정

1. 출발 노드 설정
2. 출발 노드 기준으로 각 노드 최소비용 저장
3. 방문 안한 노드 중에 가장 비용 적은 노드 선택
4. 해당 노드를 거쳐서 특정한 노드로 가는 경우를 고려해 최소비용 갱신
5. 3~4번 반복



### 구현 방법

1. 배열로 구현할 시 시간복잡도 O(N제곱)
2. 힙 쓰면 O(N * logN)



```python
import sys,heapq

INF = sys.maxsize
input = sys.stdin.readline

def dij(x):
    # d 배열을 INF 로 전부 준다
    d = [INF]*n
    # heap에다가 [0, 출발점] 을 넣는다.
    heapq.heappush(heap, [0,x])
    # d[출발점] = 0
    d[x] = 0
    # heap 다 빌 때까지 반복
    while heap:
        # w,x 는 현 위치까지의 거리와 현 위치
        w,x = heapq.heappop(heap)
        # nw,nx 는 x에서 nx까지 거리, x와 연결된 애
        # 불필요한 계산 줄이기 위해
        # 방문한 정점에서 또 다른 간선들 체크하면
        # 만약 연결된 간선이 겁나 많으면 시간이 많이 걸리게 된다.
        if w > d[x]:
            continue
        for nw,nx in a[x]:
            # nw 에 w를 더해줌 : 출발점에서 nx 까지 거리
            nw += w
            # 이게 기존에 기록해둔 값보다 작으면
            if nw < d[nx]:
                # 거리 갱신하고 heap에다가 걔네 넣음.
                d[nx] = nw
                heapq.heappush(heap,[nw,nx])
    return d

n,m,t = map(int, input().split())
a = [[]*n for _ in range(n)]
heap = []

for i in range(m):
    x,y,w = map(int, input().split())
    a[x-1].append([w,y-1])

ans = [0]*n
for i in range(n):
    d = dij(i)
    ans[i] += d[t-1]
    d = dij(t-1)
    ans[i] -= d[i]
print(max(ans))
```



### 풀어본 문제

- 백준 1238 - 파티



# 플로이드

모든 정점에서 모든 정점으로의 최단 경로

거쳐가는 정점 기준으로 최단거리 구함

노드를 하나씩 for문으로 돌면서 해당 노드를 거쳤을 때의 거리를 기준으로 최단거리를 계속 갱신한다.

경로 for문이 제일 상위 단계여야 누락되는게 없다.



```python
import sys
INF = sys.maxsize
#입력
N,M,X = map(int, input().split())
dist = [[INF for _ in range(N+1)] for _ in range(N+1)]
for _ in range(M):
    s,e,t = map(int,input().split())
    dist[s][e] = t

for k in range(1,N+1): #경로 for문이 가장 상위단계여야 누락x
    for i in range(1,N+1):
        if dist[i][k] != INF:
            for j in range(1,N+1):
				if i == j:
                    dist[i][j] = 0
                else:
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
                    
# 출력
max_time = 0
for i in range(1,N+1):
    max_time = max(max_time, dist[i][X] + dist[X][i])
print(max_time)
```



