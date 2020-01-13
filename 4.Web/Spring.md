# Spring


## 용어 정리.

### 파일구조 관련
- src Folder : 자바코드. RequestMapping 및 Controller 정의
- resource Folder : xml 설정. 
- pom.xml : maven 세팅 (패키지 관리)
    + xml 설정에 따라 프로젝트 및 의존성(라이브러리) 관리.
    + 내용변경시 Progress창 에서 다운로드 및 반영상태 확인 가능.

### 기능 및 역할 관련
- __DI (Dependency Injection)__ : 외부의 파일에서 클래스 간 설정을 정의.
    - DAO-Service 함수매핑 또는 JDBC 의 DB Connection 설정등 사용
    - Context.xml 의 bean 설정들을 통해서 객체를 사용함.
    - 한줄요약 : __Context.xml__ 에서 Java __객체를 생성__ 하고, __코드에서 사용__ 한다.
    
- Context : Application 에서 사용할 설정모음.
    + WAS (Web App Server) 에서 해당 컨텍스트 및 객체들의 사용관리
    + Servlet-Context, Root-Context 가 존재
        * Servlet 은 컨트롤러지역, Root 는 서버전역 단위로 사용됨.
        * DataSource (DB Connection 정보) 는 다양한 컨트롤러에서 사용되므로 Root
        * URL 맵핑등에 따라 다르게 사용되는 경우 Servlet


- bean : Context 에서 정의된 내용으로 사용될 class object. (IOC 핵심)
    + 해당 빈을 사용하여 자바코드에서 사용함.
    + 단지, 자바코드에서 바로 생성하는것이 아닌, xml 설정에서 관리. (WAS)
- WEB-INF/spring/**.xml : WAS 관련 Context 정보. (bean 세팅)





## Spring Annotaion

    함수로 동작을 정의 - 함수나 메서드에 붙여 @함수명을 이용해 사용.
    해당 동작은 사용될시 호출됨.

- 주로 특정 기능들 (RequestMapping) 을 바로 편집 가능.
- xml 등을 통해 context 관리가 되었으나, 규모가 커지면서 오히려 어려워 도입.






## 참조

- `코드로 배우는 스프링 웹 프로젝트`
- [인프런 Spring 강좌](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC_renew/#)
