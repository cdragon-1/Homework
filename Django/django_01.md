#### 첫 번째 장고 앱, part-1
- 장고 버전 확인
python -m django --version
- 프로젝트 만들기
django-admin startproject mysite
작성한 코드는 /home/mycode와 같은 Document root의 바깥에 두는 것이 좋다.
- startproject로 부터 생성
```
mysite/
  manage.py
  mysite/
    __init__.py
    settings.py
    urls.py
    wsgi.py
```
    - mysite/ 디렉토리 바깥의 디렉토리는 단순히 프로젝트를 담는 공간. 이름 변경 가능
    - manage.py: Django 프로젝트와 다양한 방법으로 상호작용하는 커맨드라인의 유틸리티
    - mysite/ 디렉토리 내부에는 project를 위한 실제 Python 패키지들이 저장됨. 이 디렉토리 내의 이름을 이용하여, (mysite.urls 와 같은 식으로) project 어디서나 Python 어디서나 Python 패키지들을 import 할 수 있다.
    - mysite/__init__.py: Python으로 하여금 이 디렉토리를 패키지처럼 다루라고 알려주는 용도의 단순한 빈 파일
    - mysite/settings.py: 현재 Django project의 환경/구성을 저장한다.
    - mysite/urls.py: 현재 Django project의 url선언을 저장한다. Django로 작성된 사이트의 "목차"라고 할 수 있다.
    - mysite/wsgi.py: 현재 project를 서비스하기 위한 WSGI호환 웹 서버의 진입점

- 개발 서버
python manage.py runserver
서버 동작 확인. migrations에 대한 경고들은 무시해도 됨.
    - 포트 변경 : python manage.py runserver 8080
    - 포트와 아이피 변경
      : python manage.py runserver 0.0.0.0:8000
runserver의 자동 변경 기능 : 개발 서버는 요청이 들어올 때마다 자동으로 Python코드를 다시 불러온다. 코드의 변경사항을 반영하기 위해서 굳이 서버를 재기동하지 않아도 된다. 그러나, 서버를 재기동해야 적용되는 상황도 있다.

**if you meet**
> that port is already in use :
solve like this,
sudo fuser -k 8000/tcp
port 800번과 관련된 모든 프로세스를 kill한다.
---
##### 설문조사 앱 만들기

- project vs app
  - app : 블로그나 공공 기록물을 위한 데이터베이스나, 간단한 설문조사 앱과 같은 특정한 기능을 수행하는 웹 어플리케이션
  - project : 이런 특정 웹 사이트를 위한 app들과 각 설정들을 한데 묶어놓은 것.
  > projet는 다수의 app을 포함할 수 있고, app은 다수의 project에 포함될 수 있다.

python manage.py startapp polls
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

- polls/view.py 에 첫번째 뷰 작성
view를 호출하려면 이와 연결된 url이 있어야 하는데, 이를 위해 URLconf가 사용된다.
polls 디렉토리에서 URLconf를 생성하려면, urls.py라는 파일을 생성해야 한다.

- polls/urls.py 에 포함되어야 하는 코드
```
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```
- project 최상단의 URLconf에서 polls.urls 모듈을 바라보게 설정해야 한다. mysite/urls.py 열어서, django.conf.urls.include를 import해야함. 그리고 urlpatterns 리스트에 include()함수를 다음과 같이 추가
```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
]
```
- include() 함수는 다른 URLconf를 참조할 수 있도록 도와준다. include()함수를 위한 정규 표현식에서 끝을 의미하는 기호로 $ 대신 슬래시(/)가 붙는다는 점을 기억할것. Django가 include()를 만나게 되면, 그 시점까지 일치하는 URL의 부분을 잘라내고, 남은 부분을 후속 처리를 위해 include 된 URLconf로 전달한다. 즉, /polls/some/method를 요청받으면, some/method가 polls/urls.py의 URLconf로 넘어간다.

_언제 include()를 사용해야 할까?_
admin.site.urls 를 제외한, 다른 URL패턴을 include할 때마다 항상 include()를 사용해야 한다.

- index view 가 URLconf와 잘 연결됐는지 확인
python manage.py runserver
브라우저에서 http://localhost:8000/polls/ 입력하면 확인 가능
- url()함수에는 4개의 인수가 전달되었다. 두 개의 필수 인수로 regex와 view가 있고, 두 개의 옵션 인수로 kwags와 name이 있다.
  * url() 인수: regex
  "regex"는 보통 정규 표현식을 짧게 줄여 쓰는 표현이다.문자열의 패턴을 일치시키는 문법을 말하며, 이 경우에는 url의 패턴을 찾아내는데 사용되었다.
  * url() 인수: view  
  Django 에서 일치하는 정규 표현식을 찾아내면, HttpRequest 객체를 첫번째 인수로 하고, 정규표현식에서 "잡힌" 값들을 나머지 인수로 하여 특정한 view함수를 호출한다. 만약 정규표현식이 간단한 형식이라면, 잡힌 값들은 단순히 순서 기반의 인수로서 함수에 넘겨진다. 만약 이름 기반의 정규표현식이라면, 잡힌 값들은 키워드 인수들로 함수에 넘겨진다.
  * url() 인수: kwargs
  임의의 키워드 인수들은 목표한 view에 사전형으로 전달된다.
  * url() 인수: name  
  URL에 이름을 지으면, 템플릿을 포함한 Django 어디에서나 명확하게 참조할 수 있다. 이 강력한 기능을 이용하여, 단 하나의 파일만 수정해도 project 내의 모든 URL 패턴을 바꿀 수 있도록 도와준다.

_출처 : django Documentation 공식 사이트_
