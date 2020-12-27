# JS 공부

### html 빠르게 마크업

- `+ `옆에

```html
div > ol + ul
```

```html
<div>
    <ol></ol>
    <ul></ul>
</div>
```

- `*` 여러개

```html
ul>li*5
```

```html
<ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
</ul>
```

- `^`부모의 형제노드

```html
div>ul>li^ol
```

- `()` 그룹화

```html
div>(header>ul>li*2>a)+footer>p
```

```html
<div>
    <header>
      <ul>
        <li><a href=""></a></li>
        <li><a href=""></a></li>
      </ul>
    </header>
    <footer>
      <p></p>
    </footer>
 </div>
```

- `{}` 태그안에 텍스트

```html
p{hello}
```

```html
<p>hello</p>
```

- `$` 번호매기기

```html
p.class${item $}*5
```

```html
<p class="class1">item 1</p>
  <p class="class2">item 2</p>
  <p class="class3">item 3</p>
  <p class="class4">item 4</p>
  <p class="class5">item 5</p>
```

- `>lorem` 랜덤텍스트

```html
p>lorem
```

```html
<p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Velit enim similique rem sit voluptatum aut architecto libero, corporis praesentium quae omnis? Quos dolore aperiam corporis quis quo suscipit aliquid dicta!</p>
```

```html
p>lorem4
```

```html
<p>Lorem ipsum dolor sit.</p>
```

