# 객체 지향 프로그래밍

> 세상 -> 코드

객체는 type, attribute, method를 가진다.

객체는 사람같은 거다. 

- type : 종류 - 사람에는 백인,흑인,황인 등이 있다.
- attribute : 속성 - 사람은 키는 몇 cm이고, 시력은 몇이고 이런거
- method : 함수 - 사람이 공을 던진다. 걷는다

> 객체 지향 프로그래밍은 객체가 중심이 되는 프로그래밍이다.

장점: 코드가 직관적이고, 활용이 편하고, 변경하기 편하다.



## 클래스

> 내가 원하는 attribute,method를 가진 type을 만든다.

> 이 type을 활용해서 여러 객체를 생성해서 써먹을 수 있다.



## 인스턴스 & 클래스 변수

#### 인스턴스 변수

각 인스턴스들의 속성

#### 클래스 변수

클래스의 속성, 해당 클래스의 모든 인스턴스가 공유



## 이름 탐색 순서

인스턴스와 클래스에 같은 속성 이름이 있으면, 속성 조회는 인스턴스를 우선함.

인스턴스 -> 클래스 -> 상위 클래스



## 인스턴스 & 클래스 메소드

#### 인스턴스 메소드

- 클래스 내부에 그냥 def로 선언하면 인스턴스 메소드가 됨.
- 호출 시, 첫번째 인자로 인스턴스 자기자신 `self`이 전달됨

#### 클래스 메소드

- 클래스가 사용할 메소드
- `@classmethod` 데코레이터를 사용하여 정의
- 호출 시 , 첫 번째 인자로 클래스 `cls` 가 전달됨

```python
class MyClass:
    @classmethod
    def cls_method(cls,arg1,arg2)
```

#### 스태틱 메소드

- 클래스가 사용함
- `@staticmethod` 붙여야함
- 호출시, 어떠한 인자도 전달 안됨

#### 메소드 사용시 주의할 점

- 인스턴스는 클래스,스태틱 메소드는 호출 안해야 함.
- 클래스는 인스턴스 메소드 호출 ㄴㄴ
- 클래스,스태틱 메소드 차이점: 클래스는 클래스 내 속성 같은데 접근할 때 쓰고 그게 아니면, 스태틱 메소드 쓰면 됨.

## 상속

> 부모 클래스의 모든 속성이 자식 클래스에 상속되서 중복 부분을 많이 줄일 수 있다.

```python
class son(mom):
```

#### `super()`

- 자식 클래스에 메소드를 추가로 구현할 수 있다.
- 부모 클래스 내용 쓸라면 `super()`를 쓰면 된다.

```python
class son(mom):
    def method(self, arg):
        super().method(arg)
```

#### 메소드 오버라이딩

> 자식 클래스에서 부모 클래스의 메소드를 재정의 하는 것

```python
class mom:
    def hi(self):
        print('hi')
        
class son(mom):
    def hi(self):
        print('hello')
```

이런 식으로 하면, son 인스탄스는 hello로 인사하고 mom의 인스탄스는 hi로 인사한다.

#### 다중 상속

> 2개 이상 클래스 상속 가능

```python
class son(mom,dad):
```

이때 순서가 중요하다. 맨 왼쪽에 있는 클래스의 속성을 가져온다.