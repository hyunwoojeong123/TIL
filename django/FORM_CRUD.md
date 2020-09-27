# FORM_CRUD

한 함수에서 `if` 를 사용해서 폼을 올려놓고, 폼 입력 받아서 DB에 데이터 올리는 것 둘 다 할 수 있다.

### 1. 데이터 DB에 올리기

데이터 올리는 거는 `POST`를 쓰기 때문에

1) `if request.method == 'POST':` 이 밑에다가 데이터 올리는 처리를 해주면 된다.

2) 데이터 올리는 것은 `form = ArticleForm(request.POST)` 이렇게 하면 POST로 받은 정보가 form에 담겨 있다.

3) 얘를 `is_valid()`로 유효성 검사를 해주고 유효하면

4) `form.save()`를 해서 데이터를 DB에 올린다.

**모델 폼을 사용할 때는 `article = form.save()` 하면 article에 해당 모델(데이터)가 담긴다.**

5) 그 다음 보내고 싶은데로 보내면 된다.

### 2. 입력 폼 띄우기

입력 폼 띄울 때는 `request.method`가 `POST`가 아니다.

1) 1번의 if 절에 이어 else 써주고

2) `form = ArticleForm()`빈 폼을 만든 후에

3) 걔를 context에 담아서 render로 template에 보낸다. 



**Update는 Create이랑 비슷한데, 폼에다 `(instance = article)` 이렇게 담아줘서 한다. 왜냐면, 해당 품목의 정보를 담은 상태에서 수정하는 것이기 때문**



### 3. delete하기

> delete는 DB를 수정하기 때문에 `require_post` 써서 `POST`만 받아야 한다.

article에 지울려는애 담고, `article.delete()` 써서 지운다.