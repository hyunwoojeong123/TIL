# this 바인딩

클래스 안에서 예를 들어,

```js
this.field.addEventListener('click', this.onClick);
```

요런식으로 하면 제대로 작동을 안한다.

왜냐면, 콜백으로 this.onClick을 넣었지만 함수를 인자로 어딘가에 전달할 때 클래스 정보가 전달이 안되기 때문이다.

### 그러면 어떻게 해야할까?

함수를 클래스와 바인딩 해줘야 한다. 이를 this 바인딩이라 한다.

#### 1. 

```js
this.onClick = this.onClick.bind(this);
```

클래스와 함수가 바인딩 되어서 이 onClick을 전달하면 this가 이 클래스인 걸 알게 된다.

그러나 이렇게 일일이 작성하는 방법은 안씀



#### 2. arrow function 사용

```js
this.field.addEventListener('click', (event) => this.onClick(event));
```

하나의 콜백을 감싸서 arrow function 활용



#### 3. 클래스 안에 있는 함수를 다른 콜백으로 전달할 때는 그 함수 자체를 arrow function으로 선언하는 방법

```js
onClick = event => {어쭈구저쩌구}
```

