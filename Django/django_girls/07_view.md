#### 뷰 만들기
뷰는 어플리케이션의 "로직"을 넣는 곳이다. 뷰는 앞 챞터에서 만들었던 모델에게서 필요한 정보를 받아와서 템플릿에 전달하는 역할을 한다.
blog/views.py
```
 from django.shortcuts import render
 def post_list(request):
     return render(request, 'blog/post_list.html', {})
```
>방금 우리는 post_list라는 메서드를 만들었습니다. (def가 메서드를 만들 때 사용하는 키워드였죠?) 그리고 이 메서드는 요청(request)을 넘겨받아 render 메서드를 호출합니다. render 메서드는 넘겨진 요청(request)과 blog/post_list.html 템플릿 받아 리턴된 내용이 브라우저에 보여지게 됩니다.
