# Segment Tree

> 수시로 바뀌는 수열의 구간 합을 O(log N)만에 구할 수 있다

## 시간 복잡도

- 구간 합 구하기 O(logN)
- 값 업데이트하기: O(logN)

## 공간 복잡도 : O(2**(log2(N))+1)

간단하게 O(4*N)으로 해도 됌

## 설명

트리에 자식들에 왼쪽 트리는 왼쪽 반절을 오른쪽 트리는 오른쪽 반절을 저장시킨다

구간합찾을때 범위에 따라 밑으로 죽 내려가면서 포함되는 것들만 포함한다

업데이트도 마찬가지 이러면 둘다 O(logN) 걸림



## 코드

```python
segment_tree = [-1 for _ in range(2**(math.ceil(math.log2(N)+1))+1)]

def make_segment_tree(tidx, st,ed):
    if st == ed:
        segment_tree[tidx] = arr[st]
        return segment_tree[tidx]
    else:
        mid = (st+ed) // 2
        segment_tree[tidx] = make_segment_tree(tidx*2,st,mid) + make_segment_tree(tidx*2+1,mid+1,ed)
        return segment_tree[tidx]

## arr의 idx를 val로 업글
def update_segment_tree(idx,val,tidx,st,ed):
    # print('update_segment_tree({},{},{},{},{})'.format(idx,val,tidx,st,ed))
    diff = val - arr[idx]
    if st <= idx and idx <= ed:
        segment_tree[tidx] += diff
        mid = (st+ed) // 2
        if st != ed:
            update_segment_tree(idx,val,tidx*2,st,mid)
            update_segment_tree(idx,val,tidx*2+1,mid+1,ed)
    else:
        return
# 얘 수행하고 arr[idx] = val 해줘야대

# st 부터 ed까지의 합
def sum_segment_tree(st,ed,tidx,tree_st,tree_ed):
    # print('sum_segment_tree({},{},{},{},{})'.format(st,ed,tidx,tree_st,tree_ed))
    # 구간이 아예 안 겹치는 경우
    if ed < tree_st or st > tree_ed:
        return 0
    # 트리구간이 구간 안에 완전 포개지는 경우
    elif st <= tree_st and tree_ed <= ed:
        return segment_tree[tidx]
    # 구간에 걸쳐서 겹치는 경우
    else:
        tree_mid = (tree_st + tree_ed) // 2
        return sum_segment_tree(st,ed,tidx*2,tree_st,tree_mid) + sum_segment_tree(st,ed,tidx*2+1, tree_mid+1,tree_ed)

```



## 2차원 세그먼트

