# 투 포인터

배열의 구간합을 구해야 하는경우, 2중 for문으로 쉽게 구할 수 있지만, 그럴 경우에 O(N제곱) 만큼의 시간이 걸린다.

그러나 투 포인터를 써서 하면 O(N)으로 시간을 많이 줄일 수 있다.

start,end 위치를 변경하면서 합을 계속 바꿔주고 조건에 맞으면 ans에 더하고 이런식으로 한다.

### 예시 : 수들의 합2

```python
N, M = map(int,input().split())
arr = list(map(int,input().split()))
start = end = hab = ans = 0

while True:
    if hab == M:
        #print(start,end)
        ans += 1

    if hab >= M:
        hab -= arr[start]
        start += 1
    elif end == N:
        break
    elif hab < M:
        hab += arr[end]
        end += 1


print(ans)
```



### 풀어본 문제

-  카카오 2020 인턴 - 보석 쇼핑
- 백준 2003 - 수 들의 합 2