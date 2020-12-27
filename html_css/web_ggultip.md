- css transform을 쓰면 렌더할 때 composite만 해서 성능에 좋다. top,left 사용하는거보다 좋으니까 이거 위주로 쓰자.
- 렌더할 때 페인트나 레이아웃을 다시하게되면 좀 시간이 걸린다. 애니메이션 줄 때 최대한 안 쓰게 하자.

- 사용자 부드러운 경험 위해 1초당 60개 프레임 즉, 이베트 처리하고 업데이트 될 때 16ms 안에 이루어져야한다.

- 구글 개발 툴에 performance에서 성능을 측정할 수 있다.
- 구글 개발툴에서 ctrl + shift + p 하면 panel들 볼 수 있다. 유용한 것들 많음
- css에서 *의 box-sizing을 잘 고려해야한다. {링크}[https://developer.mozilla.org/ko/docs/Web/CSS/box-sizing]

- css gradient.io 가면 gradient만들기 쉬움

- li의 css에서 overflow-y를 auto로 해주면 목록이 많아지면 스크롤바 생김
- 이벤트 위임으로 간단하게 짜자

## 코드 리팩토링

모듈화

