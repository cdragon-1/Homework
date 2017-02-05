#### 첫 번째 장고 앱, part-7, 관리 사이트 개별화
- 관리 폼 개별화하기
admin.site.register(Question)로 Question 모델을 등록하면 장고는 기본 폼을 만들어 준다. 그러나 사용자의 입맞에 맞게 모양과 동작을 바꾸고 싶다면, 객체를 등록할 때 장고에게 원하는 옵션을 전달하면 된다.
예시) admin.site.register(Question) 변경하기
```
polls/admin.py
rom django.contrib import admin

from .models import Question

class QuestionAdmin(admin.ModelAdmin):
    fields = ['pub_date', 'question_text']

admin.site.register(Question, QuestionAdmin)
```
- 모델의 관리 옵션을 변경할 때는 언제나 위와 같은 순서로 한다.
  * 첫째, 모델 관리 클래스를 생성한다.
  * 둘째, 그것을 admin.site.register()의 두 번째 인수로 넘긴다.
- 필드가 많은 폼은 fieldsets으로 분리하면 좋다.
```
polls/admin.py 예시
class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date']}),
```
fieldsets에서 각 튜플의 첫 요소는 필드셋 제목이다.
- 관련 객체 추가하기
```
polls/admin.py
from django.contrib import admin

from .models import Choice, Question


class ChoiceInline(admin.StackedInline):
    model = Choice
    extra = 3


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline]

admin.site.register(Question, QuestionAdmin)
```
- 인라인 관련 객체를 표 형식으로 표시하기
```
polls/admin.py
class ChoiceInline(admin.TabularInline):
    #...
```
- 변경 목록 페이지 바꾸기(list_display)
이것은 변경 목록 페이지에 표시할 필드 이름들의 튜플로서 열로 표시된다.
```
polls/admin.py
class QuestionAdmin(admin.ModelAdmin):
    # ...
    list_display = ('question_text', 'pub_date')
```
- 장고 소스파일 찾기
python -c "import django; print(django.__path__)"

_출처 : django Documentation 공식 사이트_
