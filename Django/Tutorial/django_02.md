#### 첫 번째 장고 앱, part-2
##### 데이터베이스 설치
- mysite/settings.py 파일 열어보기
- 기본적으로 SQLite을 사용하도록 구성되어 있음.
- INSTALLED_APPS는 현대 Django 인스턴스에서 활성화된 모든 Django 어플리케이션들의 이름이 담겨있다. App들은 다수의 project에서 사용될 수 있고, 다른 project에서 쉽게 사용될 수 있도록 패키지하여 배포할 수 있다.
INSTALLED_APPS는 Django와 함께 딸려오는 다음의 app들을 포함한다.
```
django.contrib.admin – 관리용 사이트

django.contrib.auth – 인증 시스템

django.contrib.contenttypes – 컨텐츠 타입을 위한 프레임워크

django.contrib.sessions – 세션 프레임워크

django.contrib.messages – 메세징 프레임워크

django.contrib.staticfiles – 정적 파일을 관리하는 프레임워크
```
- python manage.py migrate
migrate 명령은 INSTALLED_APPS의 설정을 탐색하여, mysite/settings.py의 데이터베이스 설정과 app과 함께 제공되는 데이터베이스 migrations에 따라, 필요한 데이터베이스 테이블을 생성한다.
---

##### 모델 만들기
: 모델이란, 부가적인 메타데이터를 가진 데이터베이스의 구조를 말한다.
polls/models.py파일 수정
```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
##### 모델의 활성화
- project에게 polls app이 설치되어 있다고 알림
```
mysite/settings.py
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
- python manage.py makemigrations polls
```
Migrations for 'polls':
  polls/migrations/0001_initial.py:
    - Create model Choice
    - Create model Question
    - Add field question to choice
```
makemigrations을 실행시킴으로서, 모델을 변경시킨 사실과 이 변경사항을 migration으로 저장시키고 싶다는 것을 Django에게 알려준다.
migration은 Django가 모델(즉, 데이터베이스 스키마를 포함한)의 변경사항을 저장하는 방법으로써, 디스크상의 파일로 존재한다.
- python manage.py sqlmigrate polls 0001_initial
: migration이 내부적으로 어떤 SQL 문장을 실행하는지 살펴보려면 실행
- python manage.py migrate
```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, polls, sessions
Running migrations:
  Rendering model states... DONE
  Applying polls.0001_initial... OK
```

- migrate 명령은 아직 적용되지 않은 모든 migration 들을 수집하여 이를 실행한다. 이 과정을 통해 모델에서의 변경 사항들과 데이터베이스의 스키마의 동기화가 이루어진다.
- 모델의 변경을 만드는 3단계 지침
```
(models.py 에서) 모델을 변경한다.

python manage.py makemigrations 을 통해 이 변경사항에 대한 migration 을 만든다.

python manage.py migrate 명령을 통해 변경사항을 데이터베이스에 적용한다.
```
migration을 만드는 명령과, 적용하는 명령이 분리된 이유는 버전관리 시스템에 migration을 커밋할 수 있게 하여 app과 함께 제공하기 위해서이다.

---
##### API 가지고 놀기
- python manage.py shell

##### 관리자 생성하기
```
python manage.py createsuperuser
Username: admin
Email address:
Password:
```
- 개발자 서버 실행
python manage.py runserver
http://127.0.0.1:8000/admin/ 으로 접근할 수 있다.
- poll app 이 보이게 하려면
polls/admin.py 파일을 열어서
```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
위와 같이 편집한다.
관리자 모드에서 데이터베이스에 저장된 질문들을 수정, 삭제, 저장할 수 있다.

_출처 : django Documentation 공식 사이트_
