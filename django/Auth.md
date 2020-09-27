# Auth

> 사용자 인증 및 권한, 다른 사람인 척 못하게 세션 기반 인증

- 장고는 인증에 관련한 폼들을 제공한다.

`from django.contrib.auth.forms import UserCreationForm,~~~`

회원가입(UserCreationForm), 로그인(AuthenticationForm), 회원정보수정(UserChangeForm)



- `get_user_model()`

얘는 현재 사용하고 있는 유저모델을 가지고 온다. 얘를 User에 담아서 views.py에서 쓴다.



- `from django.contrib.auth import login,logout`

얘네는 걍 가져다 쓰면 view의 login함수랑 이름이 똑같아서 장고가 헷갈려 한다. 그래서 `as auth_login` 이렇게 써야 한다.



- `auth_login`

얘는 쿠키,db에 session_id를 만들어서 로그인한 표시를 한다.

얘는 인자를 `auth_login(request,form.get_user())` 이렇게 좀 특이하게 준다.

request에 폼에서 받은 user를 연결 시킨다고 생각하면 된다.



- AuthenticationForm

얘는 인자를 좀 특이하게 받는다. `AuthenticationForm(request,request.POST)` 이렇게 받는다. 로그인할 때 request에 유저 정보를 담기 때문에 request를 인자로 주나 보다.



- auth_logout

얘는 쿠키,db에서 모두 session_id를 삭제한다.

`auth_logout(request)` 이렇게 쓴다.

`request.user.is_authenticated`를 써서 로그인한애만 로그아웃시키고 index페이지로 보낸다.



- `is_authenticated`

얘는 method가 아니라 user객체의 속성이다. 사용자가 인증되었는지 확인한다.

User에 항상 True이고 AnonymousUser에 대해서만 항상 False 이다.



- `@login_required`

얘는 로그인 했는지 확인하는 데코레이터이다. 로그인 안한 애들은 settings.LOGIN_URL 에 설정된 경로로 redirect 시킨다.

LOGIN_URL 의 기본값은 `/accounts/login/`

이래서 앱 이름 accounts로 하고 로그인은 login으로 한 거다.



- Password

비번을 db에 걍 저장하면 db털렸을 때 비번도 다 털린다. 그래서 해시함수 써서 비번 감춘다.

> 여기부터 다시

