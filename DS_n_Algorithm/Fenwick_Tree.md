# Fenwick Tree

> 수시로 바뀌는 수열의 구간 합을 O(log N)만에 구할 수 있다
>
> 구현이 쉽고, 속도가 빠르다

[TOC]

## 시간 복잡도

- 구간 합 구하기 O(logN)
- 값 업데이트하기: O(logN)

## 공간 복잡도 : O(N)

## 설명

![image-20210930181522279](C:\Users\Woo\AppData\Roaming\Typora\typora-user-images\image-20210930181522279.png)

## 코드

```python
tree = [0 for _ in range(N+1)]

def update(i, val):
    # print('update({},{})'.format(i,val))
    # arr의 i번째 값을 val로 바꿈
    diff = val - arr[i]
    arr[i] = val
    # LSB를 게속 더해준다
    while i <= N:
        tree[i] += diff
        i +=  (i&-i)

def hab(i):
    # LSB를 계속 뺴준다
    res = 0
    while i > 0:
        res += tree[i]
        i -= (i&-i)
    return res

def guganhab(i,j):
    return hab(j) - hab(i-1)
```



## 2차원 펜윅

