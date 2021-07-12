# REACT 기초

> react는 component들로 이루어져 있다. 프레임워크가 아니라 UI를 만드는 라이브러리

### Class vs Function

- Class는 상태가 있고 그 상태가 바뀌는 components들, lifecycle methods 사용 가능
- Function은 상태가 없는 정적인 components들



### Component

state가 업데이트 되면 render함수가 다시 호출된다.



### React Hook

function에서도 state, lifecycle methods를 사용하게 해줌

class 쓰면 되는데 굳이 이거 왜 씀?

-> 클래스가 어렵기 때문에, this를 계속 붙여야 하고 this binding issue가 있음

functional programming을 react에 도입하기 위해서 생김



### public vs src

- public에는 정적인 애들, src에는 동적인 애들이 들어간다.