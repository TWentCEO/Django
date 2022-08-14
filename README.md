# Django
-----------

## 1. MVT
<img src = "https://velog.velcdn.com/images%2Finyong_pang%2Fpost%2Fceca2333-2d78-4274-beb8-03994c6fc825%2Fimage.png" />

### MVC & MTV

* Model
  
  * 저장하고 있는 데이터의 필수적인 필드와 동작을 포함
  * 일반적으로, 각각의 모델을 하나의 데이터베이스 테이블에 매핑
  
* View
  *  사용자의 요청을 처리하고 결과를 반환하기 위한 로직을 캡슐화한 개념
* Control, Template(Django)
  * 사용자에게 표시할 정보를 표현하기 입력과 이벤트에 반응하여 Model과 View를 업데이트


<p align="center">
<img src = "https://velog.velcdn.com/post-images%2Finyong_pang%2F715ba150-20a3-11ea-9a5b-d1c6e9e9dfde%2Fimage.png" /></p>

[출처](https://velog.io/@inyong_pang/Django-Intro)

1. 웹 브라우저에서 이벤트 발생 시
(ex. 특정 url 클릭, form에 data 입력 등의 액션)
Django 서버로 request(이벤트에 대한)가 들어온다
2. Django 서버로 들어온 이벤트에 대해 URL Dispatcher가 URL을 분석해서 적합한 View로 요청을 보낸다.
3. View는 사용자 요청을 받아 Database의 어디에 접근해서 어떤 data를 가공할 건인지 Model에게 알려준다
4. Model은 Database와 연결하여 필요한 Database 연산을 처리한다.
5. Database가 다시 Model로 결과값을 보내주면 Model이 이것을 View로 전달한다
View는 우리에게 보내줄 데이터를 다시 Template에게 전달한다
6. Template는 .js나 .html과 같은 페이지를 만들어서 웹브라우저에게 넘겨준다
![dajngo architecture](https://velog.velcdn.com/images%2Fhamsterhamin%2Fpost%2Faa8ea37c-c0cf-4e35-97c7-1797989fac14%2Fimage.png)
--------
## 장고 기본 구조
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
* **manage.py**: Django 프로젝트와 다양한 방법으로 상호작용 하는 커맨드라인의 유틸리티 입니다
* **mysite/** 디렉토리 내부에는 프로젝트를 위한 실제 Python 패키지들이 저장됩니다. 이 디렉토리 내의 이름을 이용하여, (mysite.urls 와 같은 식으로) 프로젝트의 어디서나 Python 패키지들을 임포트할 수 있습니다.
* **mysite/__init__.py**: Python으로 하여금 이 디렉토리를 패키지처럼 다루라고 알려주는 용도의 단순한 빈 파일입니다. 
* **mysite/settings.py**: 현재 Django 프로젝트의 환경 및 구성을 저장합니다. Django settings에서 환경 설정이 어떻게 동작하는지 확인할 수 있습니다.
* **mysite/urls.py**: 현재 Django project 의 URL 선언을 저장합니다. Django 로 작성된 사이트의 “목차” 라고 할 수 있습니다.
* **mysite/asgi.py**: 현재 프로젝트를 서비스하기 위한 ASGI-호환 웹 서버의 진입점입니다.
* **mysite/wsgi.py**: 현재 프로젝트를 서비스하기 위한 WSGI 호환 웹 서버의 진입점입니다.

---------------
## MVT 패턴 코딩 순서
[내용 출처](https://velog.io/@inyong_pang/Django-MVTModel-View-Template-%ED%8C%A8%ED%84%B4)

1. 프로젝트 뼈대 만들기
프로젝트 및 앱 개발에 필요한 디렉토리와 파일 생성
2. Model(모델) 코딩하기
테이블 관련 사항을 개발(models.py, admin.py파일)
3. URLconf 코딩하기
URL 및 View 매핑 관계를 정의(urls.py 파일)
4. template(템플릿) 코딩하기
화면 UI 개발(templates/ 디렉토리 하위의 *.html 파일)
5. View(뷰) 코딩하기
어플리케이션 로직 개발(views.py 파일)

------
### 프로젝트 대 앱

프로젝트와 앱은 무엇이 다를까요? 앱은 블로그 시스템, 공개 기록 데이터베이스 또는 소규모 의견조사 앱과 같은 작업을 수행하는 웹 애플리케이션입니다. 프로젝트는 특정 웹 사이트에 대한 구성 및 앱의 모음입니다. 한 프로젝트에 여러 개의 앱이 포함될 수 있습니다. 앱은 여러 프로젝트에 있을 수 있습니다.

-----

## 설문조사 앱 만들기

```cmd 
py manage.py startapp polls
```
**polls**라는 디렉토리가 생성
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

### 첫 번째 뷰 작성하기

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

Django에서 가장 간단한 형태의 뷰입니다. 뷰를 호출하려면 이와 연결된 URL 이 있어야 하는데, 이를 위해 URLconf가 사용됩니다.

polls 디렉토리에서 URLconf를 생성하려면, **urls.py**라는 파일을 생성해야 합니다.

```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    urls.py
    views.py
```
---

``` python
# polls/urls.py
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

다음 최상위 URLconf에서 polls.urls 모듈을 바라보게 설정

```python
# mysite/urls.py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

**mysite/urls.py**에 **include()** 함수를 추가하여 다른 URLconf들을 참조할 수 있도록 도와준다.

Django가 함수 **includ()** 를 만나게 되면, URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include 된 URLconf로 전달