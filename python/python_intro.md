# 파이썬 기초

## 변수

> x = 1 일 때 x는 1이라는 뜻이 아니고 x에 1을 저장한다는 뜻이다.

- `x = y = 'ssafy'` 이런식으로 2개의 변수에 같은 값을 동시에 할당할 수 있다.
- `x,y = 1,2` 이런식으로 여러개의 변수에 여러 값 할당도 가능. 



## 데이터 타입

### (1) int - 정수

- 파이썬은 integer에서 오버플로우가 없다.

파이썬은 아주 큰 정수를 표현할 때 남아있는 메모리를 끌어다가 그 수 표현에 쓴다.



### (2) float - 실수 (중요)

> 파이썬에서 실수를 연산하는 과정에서 오류가 발생할 수 있다. 2진수를 통해 숫자를 표현하는 과정에서 생기는 오류 때문이다.

-  실수 연산

3.5 - 3.2 == 0.3 은 False로 나온다. 이런 부분을 해결하기 위해 몇가지 방식이 있다.

1. sys 모듈을 통해 처리하는 방법

`sys.float_info.epsilon`을 활용해서 두 값을 뺀 차이가 해당 값보다 작으면 같다고 본다.

2. math 모듈을 사용하는 방법

`math.isclose(a,b)`를 통해 두 값이 같은지 확인할 수 있다.



### (3) String - 문자

> '{문장}' 이렇게 쓴다.
>
> ''' {문장} ''' 이런식으로 여러줄 짜리 문장을 쓸 수 있다. 



#### String interpolation (중요)

- %-formatting

- str.format()

- f-strings (내가 쓰기에 제일 편함)

  1. 사용 방법

     ```python
     name = '현우'
     print(f'내 이름은 {name}')
     ```

     이런식으로 하면,

     ```
     내 이름은 현우
     ```

     이렇게 name에 담긴 값이 들어가게 된다.	

  2. 연산과 출력 형식 지정

     `print(f'{pi*r:.2}')` 둘째 자리에서 반올림해서 값이 나타나고 {}중괄호 안에 연산식을 넣을 수 있다. 형식 지정은 `변수:.2` ,`변수:%m` 이런식으로 한다. 

### 논리 연산자 단축 평가

1. and / or를 포함한 식에서

2. 먼저, 연산자 양 쪽이 bool로 형변환이 일어난다.

3. True or(and) True 이렇게 변환

   1. and 경우에는 첫번째 항목이 False일 경우 두번째 항목과 관련없이 무조건 False

   2. 이 경우에는 두 번째 항목을 고려하지 않고
   3. 첫 번째 항목을 다시 원래대로 형변환함.
   4. or은 처음이 True이면 뒤에 안봐도 되서 안 본다.



## 컨테이너

### 리스트

- 많이 씀,수정 삭제 가능, []로 묶음

### 튜플

- 수정 불가능, 읽기만 가능 ()로 묶어서 표현

### 셋

- 중복 원소 ㄴㄴ, {}로 묶음

-------------

> 컨테이너들도 형변환 된다.



## 변경 가능,불가능한 데이터

- 변경 불가능 데이터

  숫자,글자,참/거짓

- 변경 가능 데이터

  list,dict,set,사용자가 만든 데이터 타입

## enumerate

> 활용도가 높음

```python
lunch = ['짜장면', '초밥', '피자', '햄버거']
for idx, menu in enumerate(lunch):
  print(idx, menu)
```

이런 식으로 인덱스와 값을 함께 활용 가능.
