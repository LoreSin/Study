# 장고 정리 (v2.x)

## 설치 방법

- 파이썬 3.5 이상 권장. (장고 2.X 이상)
- 장고 버전에 따라 지원하는 파이썬 버젼이 다름. [버전정보 참조](https://www.djangoproject.com/download/)
- 파이썬에서 `pip install django` 로 설치

## 프론트 관련 지식들

1. HTML, CSS, Javascript 기본 문법 및 사용법 [w3schools](https://www.w3schools.com/)
    - 현재 프로젝트에서는 front 의 레이아웃은 [BootStrap](https://getbootstrap.com/) 사용. 

2. 템플릿 사용법 (장고에서는 JTL. jinja2 등도 지원하지만, 거의 흡사.)
3. Database 구조 및 지식들

---

## 2. 헬로월드

### 가상환경 및 장고 세팅
- 가상환경으로 격리된 장고환경 설치
    + venv 로 할 경우, `scripts/activate` 로 활성
    + venv 로 만들때 폴더명을 지정해줘도 되고, 폴더를 만들고 가상환경명을 정하고 . (닷) 을 찍어서, 현재 폴더에 생성하는 것도 가능.

- 프레임워크 기본 구성은 `jango-admin startproject 프로젝트이름` 을 입력
    + 프로젝트이름이 대표명이 된다.
    + `jango-admin startapp 앱이름` 으로, 보조적인 기능을 분할하여 관리하기 위해 사용

- 주요 파일 및 폴더구조
    + urls.py : url 주소들을 정의하고, view 를 연결하는 파일
    + views.py : 페이지의 구성물을 생성하거나, 일부 로직의 연결
    + model.py : DB 모델을 이용한 자료관리구조.
    + templates : 템플릿 파일 (주로 html 파일) 을 모아두고 관리.
    + static : 고정파일들 (이미지사진이나 css 파일등) 을 웹에서 사용할수 있게 함.

- 기본적인 서버 구동방법은 `python manage.py runserver`
    + 모델이 바뀌는 것이 아니라면, 대부분 즉시 갱신되어, 실시간으로 디버그가능.
    + 프로젝트를 관리하는 명령은 대부분 manage.py 을 통해서 실햄.

### 페이지 및 유저정보
- 템플릿 사용법
    + 기본적인 방법은 __render__ 로 html 을 사용. [기본튜토리얼 링크](https://docs.djangoproject.com/ko/2.2/intro/tutorial03/)
    + render 에서 context로 인자들에 따라 html 내용을 동적으로 변경
    + 프론트(html) 레이아웃을 위한 [부트 스트랩](https://getbootstrap.com/docs/4.3/getting-started/introduction/)

- Form (입력받기)
    + html 의 form 태그를 이용해서, 입력을 POST 로 받을수 있음.
    + 장고에서는 Form 을 __Form클래스로 작성__하여, html 코드를 최소화
    + django.forms 모듈을 사용
        + Form 클래스 (기본클래스. 상속받아 사용)
        + forms.CharField 등의 필드들을 설정
        + 필드내의 키widget 에 입력형식 (문자의 경우 TextInput, Password 등)
        [폼 알아보기](https://docs.djangoproject.com/ko/2.2/topics/forms/)

- 로그인 페이지
    + 로그인에 사용할 유저관련 DB 를 활성화 `python manage.py migrate`
    + auth DB 가 생성되어야 유저관리가 가능. `localhost/admin`
    + `createsuperuser` 을 사용하여, 관리자 계정생성
    + 사용자의 ID, Password 를 받는 폼을 생성.
    + 로그인페이지로 연결하며, 해당 Form POST 에서 __CSRF 토큰구문__을 추가.
        * POST 입력을 받는 페이지는 `{% csrf_token %}` 을 추가해야함.
    + 로그인폼의 입력이 올바른경우 (form.is_valid) 유저이름과 패스워드로 인증시도
        * 유저가 없다면, 에러 및 재입력을 위한 페이지. 
        * 유저 존재시, `login` 을 허용.
    + 유저가 인증된 경우, `request.user.is_authenticated` 를 통해 확인가능.
        * 이를 이용하여, 인증된 유저를 위한 컨텐츠나 뷰를 작성 가능.


- 사용자 등록 페이지
    + 레지스터 form 을 생성, 페이지를 생성
    + 폼에서 clean 메서드를 사용하여 필드 데이터검증가능.
        * 틀리다면 forms.ValidationError 를 발생 시킨다. (비번체크등)
        * `clean_username` 등으로 메소드를 선언하여, 특정 필드단위 검증 가능.
    + 입력이 올바르다면, User 모델을 이용하여 생성.
    + [사용자 관련정보 링크](https://docs.djangoproject.com/en/2.2/topics/auth/)
    + [사용자 인증 및 로그인관련](https://docs.djangoproject.com/en/2.2/topics/auth/default/)


- static 및 media 파일 관리
    + settings.py 에서 static 및 media 경로를 추가 (ROOT 및 )
    + urls.py 에서 static 경로 및 미디어 경로를 추가
    + __단! 이 방법은 개발용__ 임. 배포판에서는 수정되거나, 다른 방법을 사용.
    + `STATICFILES_DIRS` 및 `STATIC_ROOT` 지정
    + `python manage.py collectstatic` 으로 스태틱자산을 수집함.
        * 사이드에서 사용되는 스태틱파일에 대한 관리.
    + media 는 거의 동일하나, 해당 경로는 __유저 업로드 데이터__를 저장하는 위치가됨. 
    + 템플릿파일에서 `{% load static %}` 을 넣어 경로 사용 가능
        * `{% static 'css/main.css' %}` 등으로 css파일 가져오기 가능
        * `{% static 'media/beach.jpg' %}` 등으로 jpg파일 보여주기 가능
    + [스태틱 및 미디어파일 (업로드 포함) 정보](https://docs.djangoproject.com/en/2.2/howto/static-files/)

---

## 3. 프로덕트 (상품)
    상품을 취급하는 법. 별도의 앱을 만들어 관리함.

### CRUD 의 이해
> - Create 생성 -- __POST__
> - Retrieve 검색  / List / Search -- __GET__
> - Updata 갱신 -- PUT / Path / __POST__
> - Delete 삭제 -- __Delete__

### 모델작성

- 프로덕트용 App 생성 및 모델 작성
    + `python manage.py startapp APPNAME` 으로 앱 생성.
        * 기능별로 별도로 관리하기 위함.
        * 다른 외부 앱을 사용하거나, 앱별로 기능을 분리하여 관리할때 용이.
        * apps, models, views, admin 등 프레임이 생성됨.
        * 프로젝트에 `settings.py` 의 INSTALLED_APP 에 인스톨.
    + `django.db.models` 를 상속받은 클래스로 작성. (__DB 의 테이블__에 속함.)
    + 모델을 변경하거나 새로 작성한 경우의 방법
        1. `python manage.py makemigrations` 로 먼저 모델의 변경사항을 확인 겸 저장. (대부분 에러도 표시해줌.)
        2. `python manage.py migrate` 로 변경사항 적용.
        3. `admin.py` 에 해당 모델을 등록하여, 운영자가 관리할 수 있도록 연결.
        4. admin 페이지에서 해당 앱의 모델 관리 가능.
        5. admin 관리자에서 보이는 이름은, __str__ 로 

> - [db 모델을 정의 및 사용](https://docs.djangoproject.com/en/2.2/topics/db/models/)
> - [모델 래퍼런스](https://docs.djangoproject.com/en/2.2/ref/models/)
> - [모델 필드정보](https://docs.djangoproject.com/en/2.2/ref/models/fields/)
> - [마이그레이션 정보](https://docs.djangoproject.com/en/2.2/topics/migrations/)

### 리스트뷰 & 디테일뷰
    클래스를 이용하여, 모델정보를 보여주는 방법.
    이전에 사용한 render 는 함수형태로 페이지를 표시하는 방법이라면, 리스트뷰 등의 방법은 클래스를 가지고 뷰를 만드는 형태

- 생성한 모델 (Product) 를 사이트에서 표시하는 과정 : __ListView__, __DetailView__
    1. 뷰클래스 생성 (ListView 을 상속 받는 클래스)
    2. queryset 는 모델의 오브젝트를 할당. (Product.objects.all() 등)
    3. template_name 에는 사용할 템플릿 이름
        + queryset의 데이터는 object_list 의 변수명으로 템플릿에 적용됨.(기본)
    4. get_context_data 으로 context 오버라이딩
        + 페이지에서 추가적인 옵션이 사용할때.

> - [클래스뷰 유형 참조](https://docs.djangoproject.com/en/2.2/ref/class-based-views/)
> - [클래스뷰-제네릭 유형](https://docs.djangoproject.com/en/2.2/ref/class-based-views/generic-display)

### models.Manager
    모델의 쿼리를 직접만들거나 생성하여 사용가능

- 모델에서 사용하는 쿼리용 인터페이스.
- 하나의 모델에서 둘 이상의 매니저를 사용하여, 개별적인 동작수행도 가능.
[매니저API](https://docs.djangoproject.com/en/2.2/topics/db/managers/)

### QuerySet
    매니저의 기본동작들을 수정할때 사용.
- 쿼리 API 를 추가하거나 수정하여 사용. (수정 또는 확장)
    + all() 메소드가 특정 필드가 있는것만 사용할 경우
    [쿼리API](https://docs.djangoproject.com/en/2.2/ref/models/querysets/#queryset-api)
    
### 앱 URL 연결
    외부앱을 개별적 URL 로 관리
    합치기 위한 별도의 작업을 최소화함

- 프로젝트의 urls.py 에서, `django.urls.include` 을 이용해, 앱의 urls 파일내용적용
- path('product', include('products/urls')) 로 하위 경로명으로 설정


## 영상내용(1.11 버젼) 과 2.2 버젼과 다른점
- [파이썬 2.0 바뀐점](http://raccoonyy.github.io/django-2-0-release-note-summary/)
    + url 라우팅 문법 바뀜.
    + is_authenticated 가 기존의 함수에서 속성으로 바뀜.
    + 일부 필드의 요구 파라매터들이 생김
        * ForeignKey 는 on_delete 등의 파라매터를 기본적으로 요구함.

---

## 4. Templates

- html 등을 조작하는 방법들.
- extends + block 으로 베이스 템플릿으로 늘리는 방법.
- include + with : 변수를 넘기고, 템플릿에 해당 파일내용을 추가.
- [장고 템플릿 소개](https://docs.djangoproject.com/en/2.2/topics/templates/#variables)
- [장고 템플릿 문법](https://docs.djangoproject.com/en/2.2/ref/templates/language/)


### Base templates

- `{% extends "base.html" %} + {% block content %} {% endblock %}`
    + content.html 에 base.html 의 구조를 가져와서, 컨텐츠페이지를 완성시키는 방법
    + base.html 은 주로 html 의 골격구조 또는 css, js 등의 내용을 포함함.
- `{% include "target.html" with name='loresin' %}`
    + name 변수를 target.html 의 템플릿변수를 적용하여 페이지에 가져옴.
- `{% url 'detail' slug=instance.slug}`
    + 앱내의 다른 페이지로 이동시 (ex 상품상세페이지 => 상품목록페이지) 등에 사용.
    + urls.py 에서 해당 경로의 name을 파라매터로 넘겨서 이름을 지정함.
        * `path('/products', page, name='detail')`
- from django.urls import reverse
    + 주소를 생성할때 사용.
    + `reverse('detail', kwargs={'slug':self.slug})`
- path의 include 와 namespace
    + 프로젝트의 이름과 앱의 이름이 겹칠수 있으니 이를 관리하기 위해 namespace를 사용. 
    + 1.11 버젼 에서는 include('products/urls', namespace='products')
    + 2.X 버젼 에는 include(('products/urls', 'products')) 으로 사용.
        * 앱의 urls 와 네임스페이스를 함께 선언한다는 의미가 됨.
- url 경로를 templates 에서 바로 사용하기
    + {% url 'home' as home_url %}
    + urls.py 에서 `name='home'` 으로 지정한 경로의 주소를 home_url 변수로 가져옴.
    + 다양한 고정경로를 만들어야 할때. (navgator 등)

### 필터기능
- `{{ instance.description | truncatewords:12 }}`
    - 일부 단어들을 보여줌.
- `{{ instance.description | linebreaks }}`
    - 줄바꿈 적용
- `{{ instance.description | title }}`
    - 단어의 첫글자를 대문자화
- `{{ instance.timestamp | timesince }}`
    - 해당시간으로부터 얼마나 흘럿는가를 표시.
- `{{ instance.timestamp | data:'D d M Y' }}`
    - 시간을 표시하는 옵션을 바꿈. 
- [시간 표시 옵션들](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/#date)
- `{% cycle 'hello' 'there' 'world' %}`
    + for 구문 내에서, cycle 을 한번씩 만날때마다, cycle 내의 인자를 한번씩 바꿔줌.
- `{{ forloop.counter }}`
    + for 구문 내에서, 몇번째 루프인지 카운트됨. (1부터 시작)
- [템플릿 관련 태그 및 필터](https://docs.djangoproject.com/en/2.2/ref/templates/builtins/)

---

## 5. Bootstrap

- [부트 스트랩](https://getbootstrap.com/)
- 반응형 웹을 지원하는 css + js(자바스크립트) 묶음.

### 부트스트랩 적용
    대부분의 샘플코드를 제공하므로, 해당 부분을 사용함.
    공식문서의 component 에서 대부분의 예제코드가 존재.


### class
- container & container-fluid
    + container 는 최대 너비크기가 정해진 범위가 존재.
    + fluid 는 현재창의 크기를 기준으로 범위가 설정됨. (훨씬 넓은 화면 지원 )
- row & col
    + 행과 열을 기준으로 폭을 잡아줌.
    + 컨텐츠가 많으면, 격자형태처럼 보임.
    + 하나의 row 에 col 을 태그가 여러개 존재하면, 여러개가 다 나옴.
    + `col-12` 등으로, col 의 범위를 몇개를 사용할지를 정할수 있음. (최대 12)
    + 하나의 row 에서, col-12 합 까지만 지원. (col-1 은 1/12 폭 범위를 사용)

- no-gutters
    + 패딩 및 마진을 0으로 함. (여유 간격을 없앰.)

- order
    + order-1, order 12 등으로 표시되는 순서를 임의로 정할수 있음. 

- col-sm-12, col-md-6, col-lg-2
    + 화면의 크기에 따라 (통상적으로 픽셀크기) 폭크기를 다르게 표시
- col-auto
    + 컨텐츠 양에 따라 (글자수등) 폭 크기를 알아서 변경
- [부트스트랩의 Grid 시스템](https://getbootstrap.com/docs/4.3/layout/grid/)


### Spacing
- [Spacing (여백)](https://getbootstrap.com/docs/4.3/utilities/spacing/)

- padding 과 margin 을 이용한 여백 잡기
- ml-auto, mr-auto, mx-auto
    + margin left auto : 좌측여백으로 자동설정 (자신이 우측에 자리함.)
    + margin right auto : 우측여백으로 자동설정 (자신이 좌측에 자리함.)
    + margin x auto : x축 (좌우) 여백으로 자동설정 (자신이 중앙에 자리함.)
- 만약, 오와 열이 미묘하게 어긋난다면, margin 과 padding 이 일으킨 문제이다.


### Background-Color
- bg-primary
- bg-secondary
- bg-success
- bg-danger
- bg-warning
- bg-info
- bg-light
- bg-dark
- bg-white
- bg-transparent

### 주요 정보 링크
- [네비게이션 바](https://getbootstrap.com/docs/4.3/components/navbar/)
- [배경색](https://getbootstrap.com/docs/4.3/utilities/colors/#background-gradient)



## 6. Search View

- 쿼리를 이용해 검색뷰를 생성함. (제목 또는 내용등)
- 타 앱의 모델을 가져올 경우, 경로를 설정하여 사용.
- `Model.objects.filter(title__icontains='hat')`
    + hat 이 포함된 데이터
- `Model.objects.filter(title__iexant='hat')` 
    + hat 이 정확하게 맞는 데이터
- `?q=hat` 을 주소창에서 입력하면, request.GET 에 해당 쿼리로 받음.
- 쿼리를 이용해 템플릿에는 get_context_data 로 넘김
- get_queryset 으로 모델의 관련처리
- 쿼리를 중첩하여 적용하고 싶을땐 `from django.db.models import Q`
    * Product.objects.filter(Q|Q|Q).distinct() 등으로 적용.
    * distinct 는 중복제거
- 태그를 이용해 공통적인 특성을 넣고 싶을때는 모델에 M2M 연결관계를 추가하여 사용.
- Q 를 이용하여 해당 태그를 가진 아이템을 검색에 추가 할 수 있음.
    * `Q(title__icontains=query) | Q(description__icontains=query) | Q(price__icontains=query)`

## 7. carts

- carts 앱생성 => 카트 (장바구니 기능?) 구현
- session 을 이용한 사용자의 활동정보를 임시 보유. 
    + request.session 을 통해서 접근가능.
    + [세션 사용법](https://docs.djangoproject.com/en/2.2/topics/http/sessions/)
    + 간단하게 이야기 하자면, 임시 캐시db 에 저장하여 보유함.
    + 프로덕션에서는 별도의 메모리 또는 캐시DB 를 사용하여, 멀티프로세싱 safety 보장
    + 파일기반의 세션으로 사용도 가능.
    + 로그인한 유저의 세션정보만 보유함.
- `request.session` <= 세션정보 확인
    + 관련 메서드 `set_expiry(300)` 5분
    + 세션키 확인 `session_key` 
    + `request.session['id'] = number` 등으로

### 카트 구현
- model 작성
    + `user` : cart 정보를 가지는 사용자 정보참조 (외부키 참조)
    + `product` : M2M필드로 으로 상품을 정보를 담음
    + `total` : 총 가격
    + `updated, timestamp` : 작성 또는 갱신시간
    + admin 에서 카트관리 가능토록 추가.
- view 작성
    + `request.session` 을 딕셔너리처럼 접근하여 (인덱스에 키=값 할당) id 전송
    + cart_id 를 session 을 통해 전송 및 조회하여 처리.
    + 특정 카트가 존재시 기존 카트사용, 없으면 생성.
- CartManager : model 에서 사용될 매서드를 모아두는 클래스.
    + new : 새로운 카트 오브젝트의 생성
    + 로그인 상태에 따라, 비로그인의 데이터를 로그인한 데이터로 연결 하는 기능
    + new_or_get : 기존 로그인 유저의 카트가 존재시 가져오거나, 새로 생성(new)
- total을 계산하는 함수 작성 (signal 함수)
    + products 의 목록을 가져와서, 총 합산을 다시 넣는 함수를 작성.
    + sender, instance 및 키워드를 입력받는 가격계산 함수를 생성.
    + admin 에서 변경하여 적용시, M2M 목록을 바꾸기전의 내용이 적용되므로, `m2m_changed` 으로 연결한다.
        * m2m_changed 의 action 순서는 `pre_remove post_remove pre_add post_add`
        * 각 액션마다 연산되는 행동을 별도로 지정가능.
    + subtotal 필드를 추가하여, 상품값만을 저장하고, 다른 비용을 추가한 total 을 별도 관리 (세금 또는 배송비등의 연산이 될수 있음)
    + [signal 및 pre_save, post_save 등의 함수참조](https://docs.djangoproject.com/ko/2.2/ref/signals/#django.db.models.signals.pre_save)
- 카트의 view 를 업데이트
    + carts/urls.py 를 생성, 하위 url 을 관리.
    + products/views.py 에서 update 함수를 통해 product 를 추가, 제거
    + `products` 의 필드의 메서드로 product.id 를 추가제거 (add, remove 매서드)
- 폼을 통한 아이템 추가. (product:detail =POST with id=> carts:update)
    + product의 아이템을 카트에 추가하는 기능을 폼으로 구현.
    + product에 snippet templates 작성 => detail 페이지에 폼양식 추가. (include)
    + POST폼 템플릿 (update-cart.html) 에서 각 상품별 추가/ 제거 버튼 추가.
    + POST 요청에 현재 상품ID를 carts:update로 연결- 상품ID 의 액션을 수행
        * 기본적으로 토글형식으로 상품을 추가 - 해제 함
- 카트 보여주기
    + html 테이블을 이용.
    + cart_object 를 템플릿으로 넘겨서, 카트내의 products 를 템플릿에서 (for)완성
    + title, price, total 등의 간단한 표시 및 remove 기능을 추가.
    + 이전의 POST폼 템플릿 을 include하여, Remove 를 구현
- 폰트 및 아이콘
    + [font awesome4.7](https://fontawesome.com/v4.7.0/)

#### Cookies & Session 개념
    HTTP 가 연속적이지 않고, 상태가 유지되지 않는 연결의 단점 보완
    이러한 연속성 & 상태를 지원하는 방법들.

- __쿠키__ : 사용자 로컬 (브라우저) 에서, 서버로 보내고 받은 사용자 정보를 저장함.
    + 브라우저가 대부분 알아서 행동함.
    + 서버에서 쿠키를 만들어서 response, 사용자 request의 header에 담아 전송.
    + 주로 장바구니 내지는 팝업종료 시한 여부등.

- __세션__ : 쿠키기반의 행동이지만, __서버측에서 사용자의 정보를 관리__
    + 서버가 세션ID 를 발급, 클라이언트는 세션ID 를 받고 서버에 전송.
    + 세션ID 에 따라 세션정보를 처리

- 차이점
    + 세션은 보안면에서 상대적으로 유리 (사용자의 악의적 조작방지)
    + 클라이언트를 구분하여 서비스 제공 가능.
    + 세션은 서버의 메모리를 차지함.


## 8. Checkout Process

### 개요

1. 카트 -> 계산서 보기 (Checkout View)
    - 로그인/가입 또는 이메일 입력 (손님)
    - 배송주소
    - 결제 정보
        + 결제주소
        + 신용카드 / 지불방식
2. 결제 앱 (Billing app) / 요소
    - 결제 프로파일
        + 사용자 또는 이메일 (손님 이메일)
        + 결제처리 토큰 생성 (Stripe or Braintee)
3. 주문(Order) / 송장요소
    - 결제프로파일로 연결
    - 배송 / 결제주소
    - 카트
    - 상태 -- 배달 / 취소

### order app생성 및 구현
    python manage.py startapp orders
- 주문 모델 작성.
    + `order_id`, `cart`, `shipping_total`, `total`
    + `status` : 결제진행 상태 표기
- order 와 cart 간 연동
    + 고유 ID 생성
        * utils.py 에서 랜덤한 영소문자 + 숫자 10자리 조합으로 사용.
        * 세이브 전에 해당 ID 를 생성, 할당하여 사용. (pre_save)
    + cart 에서 아이템이 변동 order 총 가격 변경
        * post_save
    + post_order 가 개별적으로 저장될 경우에도 total 갱신 (post_save)
- decimal and float 연산
    + 기본적으로 둘다 실수형이기에, 변환이 필요.
    + 영상에서는 math.fsum 함수를 사용, 소수점은 format 처리. 
    + `decimal.Decimal` 클래스를 사용하여 형변환 하여 소수점 계산 처리
- checkout 을 위한 auth 업그레이드.
    + `python manage.py startapp accounts` 생성
    + 기존 login 및 register 관련 view 및 forms 관련 파일 이전 (view, forms, templates 등)
    + login의 url에 `?next=/cart/checkout/` 등으로, POST 또는 GET 이후 redirect
        * 해당 url 을 더 붙이고, `Enter` 를 누른뒤에 적용됨. 
    + logout 은 `from django.contrib.auth.views import LogoutView` 으로 사용.
        * 바로 로그아웃 됨. 
        * redirect 지점을 바꾸려면, settings.LOGOUT_REDIRECT_URL 의 경로를 덮어씀.
        * [로그아웃 관련](https://docs.djangoproject.com/en/2.2/topics/auth/default/#django.contrib.auth.views.LogoutView)

### billing app 생성

- 모델 생성 (BillingProgile)
    + user, email, active, update, timestamp 등
    + 사용자가 생성된후, billing 정보도 연속으로 생성. (post_save)
    + BillingProfile.objects.get_or_create 매서드로 user 를 외부키로 개체 생성
    + 추후에 결제시스템이 추가되면, 추가적인 customer_id 를 사용하게 될것임.
    + ForignKey 에서 Unique 속성 => `OneToOneField` 와 같이 동작하므로 사용.
    + User 의 post_save 에 BillingProgile 을 생성. (`get_or_create`)
- Checkout 에서 로그인되지 않은 경우
    + 유저 로그인 => 해당 BillingProfile 사용.
        * `request.build_absolute_uri` 를 이용, 보던 페이지로 redirect
    + 게스트 => 임시 GuestForm별도의 폼을 만들어서 Guest 처리
        * GuestEmail 모델 생성.
        * Guest 를 등록하기 위한 guest_register_view 및 url 생성
    + Cart + Billing 정보를 이용, Order 를 정리
        * Order 에 BillingProfile 를 외부키로 추가.
        * Cart + BillingProfile 로 Order 를 생성.
- Manager 를 이용하여, 로직을 분리

