#### Django 관리자
4단계에서 모델링한 글들을 장고 관리자에서 추가하거나 수정, 삭제할 수 있다.
blog/admin.py
```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
관리자 페이지에서 만든 모델을 보려면 admin.site.register(Post)로 모델을 등록해야 한다.
 http://127.0.0.1:8000/admin/
에서 로그인 페이지 확인

**슈퍼유저 생성하기**
python manage.py createsuperuser
