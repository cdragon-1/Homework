#### Django urls
mysite/urls.py
```
from django.conf.urls import include, url
   from django.contrib import admin

   urlpatterns = [
       # Examples:
       # url(r'^$', 'mysite.views.home', name='home'),
       # url(r'^blog/', include('blog.urls')),

       url(r'^admin/', include(admin.site.urls)),
   ]
```
url(r'^admin/', include(admin.site.urls)),
> 이 의미는 admin/으로 시작하는 모든 URL을 장고가 view와 대조해 찾아낸다는 뜻입니다. 이 경우 많은 admin URL을 포함해야 하기 때문에 작은 파일안에 모두 들어가지 않아요. 여기에 좀 더 읽기 좋고 깔끔한 방법이 있어요.

정규 표현식
```
^ 문자열이 시작할 때
$ 문자열이 끝날 때
\d 숫자
+ 바로 앞에 나오는 항목이 계속 나올 때
() 패턴의 부분을 저장할 때
^post/(\d+)/$
```
> ^post/는 장고에게 url 시작점에 (오른쪽부터) post/가 있다는 것을 말해 줍니다. ^)
(\d+)는 숫자(한 개 또는 여러개) 가 있다는 뜻입니다. 내가 뽑아내고자 글 번호가 되겠지요.
/는 장고에게 /뒤에 문자가 있음을 말해 줍니다.
$는 URL의 끝이 방금 전에 있던 /로 끝나야 매칭될 수 있다는 것을 나타냅니다.

mysite/urls.py
```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', include(admin.site.urls)),
    url(r'', include('blog.urls')),
]
```
> 지금 장고는 'http://127.0.0.1:8000/'로 들어오는 모든 접속 요청을 blog.urls로 전송하고 추가 명령을 찾을 거예요.

blog/urls.py 라는 새 파일 생성하기
```
from django.conf.urls import url
from . import views
urlpatterns = [
    url(r'^$', views.post_list, name='post_list'),
]
```

>제 post_list라는 이름의 view가 \^\$ URL에 할당되었습니다. 이 정규표현식은 ^에서 시작해 $로 끝나는 지를 매칭할 것입니다. 즉 문자열이 아무것도 없는 경우만 매칭하겠죠.
