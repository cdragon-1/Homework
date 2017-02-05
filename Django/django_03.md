#### 첫 번째 장고 앱, part-3
- view 추가하기
: view는 Django 어플리케이션이 일반적으로 특정 기능과 템플릿을 제공하는 웹페이지의 한 종류이다. 예를 들어, 블로그 어플리케이션의 경우 다음과 같은 view를 가질 수 있다.
  * Blog 홈페이지 - 가장 최근의 항목들을 보여준다.
  * 항목 "세부"(detail) 페이지 - 하나의 항목에 연결하는 영구적인 링크를 제공한다.
  * 년도별 축적 페이지 - 주어진 연도의 모든 월별 항목들을 표시한다.
  * 월별 축적 페이지 - 주어진 월의 날짜별 항목들을 표시한다.
  * 날짜별 축적 페이지 - 주어진 날짜의 모든 항목들을 표시한다.
  * 댓글 기능 - 특정 항목의 댓글을 다룰 수 있는 기능

- Django에서는, 웹페이지와 기타 내용들이 view에 의해 제공된다. 각 view는 간단한 Python 함수를 사용하여 작성된다. Django는 요청된 URL을 조사하여 view를 선택한다.
- view를 URL에서 얻기위해, Django는 URLconfs라고 부르는 것을 사용한다. URLconf는 URL 패턴(정규 표현식으로 표현)과 view를 연결한 것이다.
```
polls/views.py 예시
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```
polls.urls모듈에서 새로 작성된 view들을 연결하기 위해 아래와 같이 url()함수 호출을 추가한다.
```
from django.conf.urls import url

from . import views

urlpatterns = [
    # ex: /polls/
    url(r'^$', views.index, name='index'),
    # ex: /polls/5/
    url(r'^(?P<question_id>[0-9]+)/$', views.detail, name='detail'),
    # ex: /polls/5/results/
    url(r'^(?P<question_id>[0-9]+)/results/$', views.results, name='results'),
    # ex: /polls/5/vote/
    url(r'^(?P<question_id>[0-9]+)/vote/$', views.vote, name='vote'),
```
- 404 에러
```
polls/views.py
from django.http import Http404
from django.shortcuts import render

from .models import Question
# ...
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
```
view는 요청된 질문의 ID 가 없을 경우 Http404예외를 발생시킨다.

_출처 : django Documentation 공식 사이트_
