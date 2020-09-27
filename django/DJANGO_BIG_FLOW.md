# 장고 흐름

> 1.urls.py에 path 써서 view함수와 url 연결
>
> 2.views.py에 함수 써서 해당 url입력 받을 때 그에 맞는 동작을 하게 한다.
>
> 3.template은 HTML파일로 view에서 전달받은 context를 써서 브라우저에 페이지로 나타낸다.

### 1. urls.py 에 path 쓰기

다른 app들의 urls.py와 연결하기 위해 

**메인 프로젝트**에서

`path('articles/', include(articles.urls))` 

이런 식으로 써준다.

이때 `include`를 사용하기 위해

`from django.urls import include `

이렇게 써준다.



**앱의 urls.py** 에서는

1) 뷰 함수들을 사용하기위해`from . import views` 한다.

2) `app_name = 'articles'` app_name을 지정한다. app_name을 지정해야 나중에 url의 path들을 `articles:index` 이렇게 별명으로 부를 수 있다.

3) 별명으로 부를라면 한 가지 일을 더해야 하는데, path를 쓸 때

`path('index/', views.index, name = 'index')`

이렇게 name을 정해줘야 한다.



#### * Variable routing

path 쓸 때 `path('detail/<int:pk>/')` 이런 식으로 쓰면 pk를 view함수에 인자로 넘길 수 있다.

얘를 사용해서 특정 번호에 해당하는 article을 불러오거나 할 수 있다.



### 2. views.py 에 함수 선언하기

>  여기서는 url입력 받았을 때 그에 맞는 동작을 하는 함수를 만든다.

예를 들어서 index를 보여주는 함수는

`articles = Article.objects.all()`

이렇게 ORM을 활용해 DB에서 데이터를 불러온 후에

걔네를 `context = {'articles' : articles,}` 이렇게 context에 담아서

template에 보낸다.



#### * ORM(Object-Relational Mapping)

- 객체(Object) 와 관계형 DB의 데이터를 맵핑(Mapping) 해준다.
- 얘를 써서 SQL문 안 쓰고 장고에서 DB 데이터 불러와서 쓸 수 있다.



### 3. template으로 브라우저에 띄울 페이지 만들기

> 얘는 HTML 폴더로 브라우저에 출력할 애들이다.

context로 전달받은 애들은 `{{article}}` 이런 식으로 가져다 쓸 수 있다.

`for,if` 같은 건 요긴하게 쓴다.

`BASE_DIR` 밑에 template 만들어서 `base.html`만들고

`extends`를 사용해서 템플릿마다 가져다 쓰면 편하다.

bootstrap이랑 연결해서 꾸미는 것도 가능하다.