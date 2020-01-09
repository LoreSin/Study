# Servlet & JSP
  

## 간단한 요약
  자바언어를 이용하여 웹페이지를 만드는 자바프로그램
  WAS (톰캣, JBOSS 등) 을 통해 웹서버를 실행.

- Servlet : 요청의 처리 및 반환을 작성하는 자바코드
- JSP : HTML 로 작성된 페이지에 자바언어를 삽입, 이를 처리하여 페이지를 생성.

## MVC model 1 & 2

- Model 1
  - JSP 위주로 로직 및 처리를 진행. 간단함. 복잡하거나 큰 프로그램엔 부적합.

![모델1](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Model_1.png/390px-Model_1.png)

- Model 2
  - Servlet 은 컨트롤러 역할. 로직이 나누어져있어 분업및 확장 용이하나, 작업량과 규모가 큼.

![모델2](https://upload.wikimedia.org/wikipedia/commons/thumb/7/72/JSP_Model_2.svg/220px-JSP_Model_2.svg.png)

#### 차이점

- 모델2는 모델1의 향상된 버젼이 아닌, 프로그래밍 관점에서 "로직의 분리를 통한 유지보수성" 을 높인 모델.
- 작업량이 증가하나, 유지보수 및 로직분리 (기능분리) -> 분업 및 유지보수 용이.
      
      
## DTO & DAO

- DAO : Data Access Object
    + DB 에 접속하는 객체
    + Connection 과 SQL 쿼리문을 사용하여 DB 에서 데이터를 가져오는 처리.

- DTO : Data Transfer Object
    + DB 의 데이터를 담는 객체
    + 쿼리의 결과나 쿼리에 담는 데이터의 기본단위. (여러개의 경우는 ArrayList<DTO> 타입)
    + 역할의 유사성으로 VO (Value Object) 와 거의 같게 느끼지만 다르다.
    + DTO : mutable // VO : immutable

- 중복되는 코드제거
    + DB 접속 ~ SQL 처리등의 과정이 Servlet (또는 JSP) 에서 분리
    + 재사용성 & 유지보수 용이. (특정 기능의 코드가 모이게 됨)

- 장고모델 (Python Django ORM) 과 차이점. -개인의견-
    + ORM (Object Relation Model) 을 직접 구현 하거나, SQL 문법을 쉽게 정리하여 Class 화 하는 방법이 DAO DTO 방식으로 보임.
    + 직접 모델과 메서드를 통해서, 미리 선언된 SQL 문법으로 데이터를 받아오는 방식과 유사함.
    + ORM 과 SQL 문법을 그대로 사용하는 방식의 중간과정의 기법이라 생각됨.

## DataSource
    ConnectionPool 을 관리하는 객체

- 사용이유
    + DBMS 의 부담을 줄이기 위해, Connection 을 미리 생성하고, 해당 커넥션을 재사용
- 사용법
    + Context.lookup 을 통해 DataSource 를 불러옴.
    + DataSource.getConnection 을 통해 DB 접근.



## EL
  Expression Language
  ${expression} 으로 사용하여, 자바코드 또는 JSP 문서에 값을 `표현` 하기 위한 언어.
  Request 이나 Context 등의 값을 읽어오는데 사용되며, JSTL 와 함께 사용됨.

## JSTL
  JSP Standard tag library

- JSP 에서 사용되는 태그들의 집합.
- 기존에 사용한 자바문법을 사용할때 생기는 가독성 및 복잡성 해소.
- 현재 1.2 버젼이 사용됨.


## 참조
- `최범균의 JSP 2.3 웹 프로그래밍`
- [오픈 튜토리얼](https://opentutorials.org/module/3569/21232)
- [인프런 JSP 강좌](https://www.inflearn.com/course/%EC%8B%A4%EC%A0%84-jsp_renew)
- [jsp model1](https://en.wikipedia.org/wiki/JSP_model_1_architecture)
- [jsp model2](https://en.wikipedia.org/wiki/JSP_model_2_architecture)
