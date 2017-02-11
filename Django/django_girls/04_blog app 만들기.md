#### 어플리케이션 제작하기
manage.py startapp blog
> 어플리케이션을 생성한 후 장고에게 사용해야한다고 알려줘야 합니다. 이 역할을 하는 파일이 mysite/settings.py입니다. 이 파일 안에서 INSTALLED_APPS를 열어, )바로 위에 'blog'를 추가하세요. 최종 결과물은 아래와 다음과 같을 거에요.

    INSTALLED_APPS = (
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'blog',
    )
#### 블로그 글 모델 만들기
> 모든 Model 객체는 blog/models.py 파일에 선언하여 모델을 만듭니다. 이 파일에 우리의 블로그 글 모델도 정의할 거에요.
blog/models.py
from django.db import models
from django.utils import timezone
```
from django.db import models
from django.utils import timezone


class Post(models.Model):
    author = models.ForeignKey('auth.User')
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title
```

#### 데이터베이스에 모델을 위한 테이블 만들기
python manage.py makemigrations blog
./manage.py migrate blog
