# Union Find (disjoint-set)

서로 중복되지 않는 부분 집합들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조

다수의 노드들 중에 연결된 노드를 찾거나 노드들을 합칠 때 사용하는 알고리즘



### 구현

- 초기화 : N 개의 원소가 각각의 집합에 포함되어 있도록 초기화
- Union 연산 : 두 원소 a,b가 주어질 때, 이들이 속한 두 집합을 하나로 합침
- Find 연산 : 어떤 원소 a 가 주어질 때, 이 원소가 속한 집합을 반환



### 1. 배열 사용 방식

1. 먼저 원소의 크기만큼 배열을 초기화해준다.

2. 그 다음 두 원소를 합치기 위해 배열의 모든 원소를 순회하면서 하나의 번호를 나머지 하나로 교체.



Union 연산이 배열의 모든 원소를 순회하게 되기 때문에 시간복잡도가 O(N)이다. 이 때문에 트리 구조를 많이 사용한다.



```python
class DisjointSet:
    def __init__(self,n):
        self.data = list(range(n))
        self.size = n
        
    def find(sel,f index):
        return self.data[index]
    
    def union(self,x,y):
        x,y = self.find(x), self.find(y)
        
        if x == y:
            return
        
        for i in range(self.size):
            if self.find(i) == y:
                self.data[i] = x
                
```





### 2. 트리구조를 사용하는 방식

union-by-size, union-by-height, path comprehension 3가지 방식이 있다.

#### union-by-size : 원소 수가 적은 집합을 원소가 많은 집합의 하위 트리로 합친다.

#### union-by-height : 트리 높이가 작은 집합을 높이가 더 큰 집합의 하위 트리로 합친다.



##### union-by-size 구현

**흐름**

1. 주어진 원소의 개수만큼 사용하지 않을 값 (예제에서는 -1)을 생성
2. 루트노드의 인덱스를 찾음
3. 루트노드의 인덱스가 다르다면 리스트의 값이 더 낮은(size가 더 큰) 것을 찾아서 큰 것에 더해줌
4. 작은 건 큰 것의 인덱스로 바꿔준다.



**시간복잡도** : O(logn)

```python
class DisjointSet:
    def __init__(self, n):
        self.data = [-1 for _ in range(n)]
        self.size = n
        
    def find(self, index):
        value = self.data[index]
        if value < 0:
            return index
        
        return self.find(value)
    
    def union(self, x, y):
        x = self.find(x)
        y = self.find(y)
        
        if x == y:
            return
        
        if self.data[x] < self.data[y]:
            self.data[x] += self.data[y]
            self.data[y] = x
        else:
            self.data[y] += self.data[x]
            self.data[x] = y
            
        self.size -= 1
        
```



##### union-by-height 구현

```python
union 부분만 빼고 by-size와 같다.
def union(self,x,y):
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
    
```



##### path comprehension

union-by size,height은 find() 연산을 수행할 때 트리의 높이만큼 올라가 루트를 찾을 수 있는데, 이러한 비효율성을 해결하고자 나온 개념. find() 연산 비용을 낮출 수 있다.



1. find(x)를 실행
2. x가 루트가 아니라면 임시로 저장
3. 루트노드를 찾을 때까지 재귀함수 반복
4. 루트노드를 찾으면 x를 루트노드의 자식으로 표시



``` python
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
```



### 사용처

- Kruksal 알고리즘에 사용한다.



### 모르겠는거

- path-comprehension