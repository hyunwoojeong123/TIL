# html_data_attribute

태그들 속성으로 `data-display-name = "어쩌구"` 이렇게 쓰면 된다.

내가 원하는 데이터 값을 태그에 부여할 수 있어 좋다.



그 다음 css에서

```css
[data-display-name='dream']{
    background-color: beige;
}
```

이런 식으로 접근 가능



js에서

```js
const dream = document.querySelector('div[data-display-name="dream"]');
```

이런 식으로 접근 가능



사용자에게 민감한 데이터는 돔요소에다가 추가해서 보관 ㄴㄴ 

왜냐면 검사만 해도 다 보이기 때문에