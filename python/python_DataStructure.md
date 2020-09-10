# 데이터 구조

## 문자열(String)

> 변경할 수 없고, 순서가 있고, 순회가 가능하다.

- 가지고 있는 method를 잘 활용하면 문제를 쉽게 해결할 수 있다.

- C++이랑 다르게 String이 변경할 수 없어서, `str[i] = str[j]` 이런식으로 index 지정해서 해당 문자를 바꿀 수는 없다. 이를 구현하려면, 그냥 빈 String을 하나 선언해서 for문으로 할당하는게 낫다.

```python
str = 'apple'
# a 와 l의 위치를 서로 바꾸고 싶으면,
index_a = 0 # a의 index
index_l = 4 # l의 index
changed = ''
for i in range(0,len(str)):
    if i == index_a:
        changed += str[index_l]
   	elif i == index_l:
        changed += str[index_a]
    else:
        changed += str[i]
```



- `.split() `은 알고리즘 문제 풀 때 입력받을 때 요긴하게 쓰인다. C++은  배열 선언해놓고, for문으로 받으면 편하게 받을 수 있는데, 파이썬은 입력받는게 좀 불편하다. 변수 선언할 때 따로 type을 설정하지 않기 때문에 입력은 무조건 str으로 받는다. 따라서 숫자 같은걸 입력받으면, 해당 str을 `split() `하면, 공백문자를 구분으로 해서 list에 해당 숫자가 담긴다. 이를 map을 활용해 int로 바꿔줘야 한다. 그래도 적응만 하면 별로 어려울 건 없을 것 같다.

```python
nums = map(int, input().split())
```



 ## 리스트

> 변경 가능하고, 순서가 있고, 순회가 가능 mutable, ordered, iterable
>
> method들도 좋고, C++에서 배열 쓰듯이 쓰면 된다. 약간 vector 느낌이다.

## 딕셔너리

> mutable,unorderd,iterable
>
> C++의 구조체 같은 느낌인데 훨씬 쓰기 편하다.
>
> key와 value의 쌍으로 구성되어 있다.



## 궁금한 점

- 왜 string을 변경불가능하게 해서 불편하게 만들어놨을까