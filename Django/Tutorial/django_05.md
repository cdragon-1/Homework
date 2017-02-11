#### 첫 번째 장고 앱, part-5
- 자동화된 테스트
: 테스트 코드가 동작하는지 확인하는 간단한 루틴. 시스템이 테스트 작업을 해 준다는 점에서 일반적인 테스트와 다르다. 테스트 집합을 한번 만들어 두면 앱을 변경했을 때 코드가 원래 의도한 대로 동작하는지 쉽게 확인할 수 있다. 일일이 손으로 확인하느라 시간을 소비하지 않아도 된다.
- 테스트 작성이 필요한 이유
  * 시간을 절약해준다
  * 문제를 찾을 뿐만 아니라 예방도 한다
  * 코드의 매력을 높인다
  * 팀의 협업을 돕는다
- 테스트 실행하기
python manage.py test polls
polls 앱에 있는 bug  찾는 과정
```
Creating test database for alias 'default'...
F
======================================================================
FAIL: test_was_published_recently_with_future_question (polls.tests.QuestionMethodTests)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/path/to/mysite/polls/tests.py", line 16, in test_was_published_recently_with_future_question
    self.assertIs(future_question.was_published_recently(), False)
AssertionError: True is not False

----------------------------------------------------------------------
Ran 1 test in 0.001s

FAILED (failures=1)
Destroying test database for alias 'default'...
```
> 구체적으로는 다음 단계로 진행되었습니다.
python manage.py test polls 명령은 polls 애플리케이션에서 테스트를 찾습니다.
django.test.TestCase의 서브 클래스를 발견합니다.
테스팅에 사용할 특별 데이터베이스를 생성합니다.
테스트 메소드를 찾습니다. 이름이 test로 시작하는 메소드입니다.
test_was_published_recently_with_future_question에서 pub_date가 30일 후인 Question 인스턴스를 생성합니다.
… assertIs() 메소드를 사용하여 was_published_recently()가 True를 반환한다는 사실을 발견합니다. 원했던 값은 False입니다.

- 장고 테스트 클라이언트
장고는 뷰 수준에서 사용자의 코드 실행을 시뮬레이션해주는 테스트 Client를 제공한다. 이 Client는 test.py에서 사용할 수 있으며 심지어 shell에서도 사용할 수 있다.
  * shell에서 테스트 환경 설정
\>>> from django.test.utils import
\>>> setup_test_environment
\>>> from django.test import Client
\>>> client = Client()
여기까지 하면 테스트 준비 끝

_출처 : django Documentation 공식 사이트_
