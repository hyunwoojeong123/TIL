# Bitmasking

> 비트 단위로 k번째 물건이 선택된지 안 된지를 표현하는 기술.
>
> 껏다 키는 스위치 같은 느낌.

```python
for i in range(1, 1<<N): # 모든 경우의 수
    total = 0
    for j in range(N):
        if i & (1 << j): # j번째 자리수가 1이면, 포함한다.
            total += M[j]
    if total >= B and total < ans:
        ans = total
```

풀어볼 문제 : 백준 2098번 외판원 순회