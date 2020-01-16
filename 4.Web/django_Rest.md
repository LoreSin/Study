# Ddjango 를 이용한 Rest Framework 
  Rest API? => Json 으로 Model (DB) 을 CRUD 매핑 (get, post, update, delete) 하여 처리하는 API
  DjangoRestFramework 는 Django 모델을 이용하여 Rest API 를 지원하도록 만드는 심플라이저
  
- 첫 튜토리얼 참조 사이트.
- [RestFramework 공식샘플](https://www.django-rest-framework.org/#requirements)
- [gunicorn 및 nginx 세팅](https://wikidocs.net/6601)
- [파이썬 WAS 구축하기](http://dveamer.github.io/backend/PythonWAS.html)
  
  
## 요구 사항 및 간단 요약

- python3 설치
- pip 로 django, djangorestframework, serializers
  - settings 의 INSTALLED_APPS 에  rest_framework 추가. (djangorestframework 의 이름)
  - serializers 는 json 으로 응답을 변환. 
  - 
- centos7 에서는 sqlite 및 


## Gunicorn
  Gunicorn : 파이썬의 WSGI HTTP 서버
  WSGI : Web Server Gateway Interface. 즉, 웹서버를 `파이썬 프로그램` 이 연결되게 인터페이스규격
  즉, Gunicorn 은 WSGI 의 구현체. (uWSGI 등 존재)

- [Gunicorn 공식사이트](https://gunicorn.org/)
- 설치 `pip install gunicorn`
- 기본 사용 명령어 `gunicorn -w 3 myapp:app`
  - 인자 w = worker 개수 (프로세싱 개수)
- 일반적으로는 `/etc/systemd/system/gunicorn.service` 에서 시스템을 등록. (자동 실행 및 세팅)


## nginx
  nginx : 비동기식 웹서버 소프트웨어
  gunicorn 과 nginx : Gunicorn 통하여 WSGI 구현 앱을 웹으로 서비스 함.
  

- [nginx 위키](https://ko.wikipedia.org/wiki/Nginx)


