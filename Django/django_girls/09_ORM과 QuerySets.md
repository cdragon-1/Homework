#### ORM과 QuerySets
- QuerySets : 전달받은 모델의 객체 목록. 데이터베이스로부터 데이터를 읽고, 필터를 걸거나 정렬할 수 있다.
- ORM : (Object Relational Mapping)은 논쟁을 끌고 다니는 기술입니다. 지지자들은 ORM을 활용하면 생산성이 높아지고 캐시 등 다양한 저장소를 활용하기에 유연한 구조를 만들어 준다는 장점을 내세웁니다.
- 입력했던 글들 출력하기
```
from blog.models import Post
Post.objects.all()
```
- 객체 생성하기
```
from django.contrib.auth.models import User
User.objects.all()
me = User.objects.get(username='ola')
Post.objects.create(author=me, title='Sample title', text='Test')
Post.objects.all()
- 필터링하기
```
Post.objects.filter(author=me)
Post.objects.filter( title__contains='title' )
from django.utils import timezone
Post.objects.filter(published_date__lte=timezone.now())
 post = Post.objects.get(title="Sample title")
 post.publish()
Post.objects.filter(published_date__lte=timezone.now())
- 정렬하기
```
Post.objects.order_by('created_date')
[<Post: Sample title>, <Post: Post number 2>, <Post: My 3rd post!>, <Post: 4th title of post>]
 Post.objects.order_by('-created_date')
[<Post: 4th title of post>,  <Post: My 3rd post!>, <Post: Post number 2>, <Post: Sample title>]
- 쿼리셋 연결하기
```
Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
```
