#### 첫 번째 장고 앱, part-4
- HTML \<form\> 요소 추가
```
polls/templates/polls/detail.html

<h1>{{ question.question_text }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'polls:vote' question.id %}" method="post">
{% csrf_token %}
{% for choice in question.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}" />
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br />
{% endfor %}
<input type="submit" value="Vote" />
</form>
```
  > * 위 템플릿은 각 질문 선택지에 라디오 버튼을 표시합니다. 각 라디오 버튼의 value는 연관된 질문 선택지 ID입니다. 각 라디오 버튼의 name은 “choice”입니다. 즉, 누군가 라디오 버튼 하나를 선택하고 폼을 제출하면 폼은 POST 데이터 choice=#를 전송한다는 뜻입니다. 여기서 #은 선택된 항목의 ID입니다. 이것은 HTML 폼의 기본 개념입니다.
  > * 폼의 action을 {% url ‘polls:vote’ question.id %}로 지정하고 method=”post”를 설정했습니다. (method=”get”이 아니라) method=”post”라는 사실이 매우 중요합니다. 폼을 제출하는 행위가 서버쪽 데이터를 변경하기 때문입니다. 서버쪽 데이터를 변경하는 폼은 method=”post”를 사용해야 합니다. 이는 장고에만 국한된 팁이 아니라 좋은 웹 개발 관례입니다.
  > * forloop.counter는 for 태그가 루프를 반복한 횟수를 나타냅니다.
  (데이터를 수정하는 효과가 있는) POST 폼을 생성하므로 사이트 간 요청 위조(CSRF, Cross Site Request Forgeries)를 걱정해야 합니다. 고맙게도 크게 걱정할 필요는 없습니다. 장고가 사이트 간 요청 위조에 대응하는 사용이 간편한 보호 시스템을 제공하기 때문입니다. 간단히 말하면, 내부 URL로 데이터를 전송하는 모든 POST 폼은 {% csrf_token %} 템플릿 태그를 사용해야 합니다.

- vote()함수 수정
```
polls/views.py
from django.shortcuts import get_object_or_404, render
from django.http import HttpResponseRedirect, HttpResponse
from django.urls import reverse

from .models import Choice, Question
# ...
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # 설문 폼을 다시 표시합니다.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # POST 데이터를 성공적으로 처리한 후에는 항상 HttpResponseRedirect를
        # 반환합니다. 그래야 사용자가 뒤로가가(Back) 버튼을 클릭했을 때 폼이
        # 두 번 제출되는 현상이 생기지 않습니다.
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```
- 제너릭 뷰 사용하기 : 코드는 적을수록 좋다.
웹 개발에서 흔히 접하는 일반적인 시나리오일 경우 사용. 예제의 polls app은 URL로 전달된 매개변수에 따라 데이터베이스에서 데이터를 가져온 후 템플릿을 로드하고 템플릿에 데이터를 채워 반환한다. 너무도 일반적인 시나리오라 장고는 "제너릭 뷰" 시스템이라는 지름길을 제공한다. 제너릭 뷰는 앱을 만들 때 파이썬 코드를 작성할 필요가 없을 정도로 공통적인 패턴을 추상화한다.

_출처 : django Documentation 공식 사이트_
