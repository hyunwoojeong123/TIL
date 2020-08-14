# 장고

### 코드작성 순서 - 데이터 흐름. URL -> View -> template

1. urls.py
2. views.py

3. templates



### 장고 서버를 꺼야할때

새 파일 만들거나,폴더 변화 있을때 추적이 안된다.



### 장고 작업 순서

1. startproject
2. startapp
3. app 등록 - settings.py
4. url
5. view
6. template



### 변수 받기

` path('hello/<str:name>/',views.hello)`



-----



### Django Template Language (DTL)

- django template system에서 사용하는 built-in template system이다.
- 조건,반복,치환,필터,변수 등의 기능을 제공.
- 프로그래밍적 로직이 아니라 프레젠테이션을 표현하기 위한 것

- 파이썬처럼 if,for를 사용할 수 있지만 이거는 단수히 python code로 실행되는 것이 아닙니다.



syntax

- variable : `{{ }}`
- filter: `{{ variablefilter }}` 변수나 태그 뒤쪽에 붙는거 | 파이프 라인 붙이고 씀.
- tag: `{% tag %}`  





------



### 템플릿 시스템 설계 철학

- 장고는 템플릿 시스템이 표현을 제어하는 도구이자 표현에 관련된 로직일 뿐이라고 생각한다.

- 템플릿 시스템에서는 이러한 기본 목표를 넘어서는 기능을 지원해서는 안된다.



## form , method = "GET"

1. throw.html이
2. /catch/로 form으로 요청함
3. catch view함수 실행 - data
4. catch.html이 출력



### ** 공식 문서 중요

