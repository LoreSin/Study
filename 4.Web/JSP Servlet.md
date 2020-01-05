# Servlet & JSP

## 간단한 요약
  자바언어를 이용하여 웹페이지를 만드는 서버프로그램

- Servlet : 요청의 처리 및 반환을 작성
- JSP : HTML 로 작성된 페이지에 자바언어를 삽입하여, 웹페이지를 생성.

## MVC model 1 & 2

- Model 1

![모델1](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Model_1.png/390px-Model_1.png)

- Model 2

![모델2](https://upload.wikimedia.org/wikipedia/commons/thumb/7/72/JSP_Model_2.svg/220px-JSP_Model_2.svg.png)

-----

- 차이점
  - 모델1은 JSP 위주로 로직 및 처리를 진행. 간단함. 복잡하거나 큰 프로그램엔 부적합.
  - 모델2은 Servlet 은 컨트롤러 역할. 로직이 나누어져있어 분업및 확장 용이하나, 작업량과 규모가 큼.
  - 모델2는 모델1의 향상된 버젼이 아닌, 프로그래밍 관점에서 "로직의 분리를 통한 유지보수성" 을 높인 모델.
      - 생산성은 떨어짐. (작업량 증가) 유지보수 및 로직분리 (완성물의 기능적 구분) -> 분업 및 유지보수성 향상
      
    
