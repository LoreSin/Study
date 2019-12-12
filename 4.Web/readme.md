# Web 관련 간단정리

## 기본 용어들
- HTML, CSS, javascript : 웹 페이지 표현하는 기본언어
  - html : xml 기반의 구조정의 (ex. h1, p, footer 등의 태그 및 속성값)
  - css : Cascasde Style Sheet. html로 된 페이지의 모양(패딩, 마진 또는 색상등) 또는 동작(마우스클릭이나 팝업등) 정의.
  - javascript : 스크립트 프로그래밍 언어. dom 을 통해 html 을 접근하여, 그 속성을 정의. 최근에는 다양한 용도 (node.js 등) 로도 쓰임.
  - [기본문법 사이트](https://www.w3schools.com/) : 웹 및 기본문법 프로그래밍 사이트.

- 적응형 웹 (Responsive Web)
  - 다양한 사용자 디바이스 (모바일 및 데스크탑등) 의 화면크기에 따라 레이아웃이 재배치되어 화면을 제공하는 웹.
  - CSS Framework 을 사용하면 구현하기 쉬움. (Bootstrap, Material-UI, Bulma 등)
  - 부트스트랩은 각 엘레먼트가 가로로 분할된 12개의 그리드 점유갯수를 변경하는 방법을 구현 한것으로 보임.
  
- MVC 모델
  - [MVC 위키](https://ko.wikipedia.org/wiki/%EB%AA%A8%EB%8D%B8-%EB%B7%B0-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC)
  - __Model, View, Controller__ 을 뜻하는 소프트웨어 패턴.
  - UI 프로그램에서 사용 하는 기본 구조.
    - 구현된 프레임워크나 구현방법에 따라 다르게 부르기도 함. (Django - MTV 등)
    - 의존성을 낮춘 MVP, MVVM 같은 모델도 존재함.
  - 각 기능을 분리하여, 분업과 유지보수를 쉽게 함.
  - 기능을 간단하게 구분하면
    - Model : 데이터 관리 (비즈니스 로직)
    - View : 화면 처리 (레이아웃 또는 유저의 입력 버튼등)
    - Controller : 유저의 명령을 확인, Model 과 View 로 넘김.



## Django?
  Python 을 이용한 Web Framework

- MTV 구조로, Model, Template, View 으로 구성. MVC 와 거의 대응.
  - Model 은 동일
  - Template 는 Html 페이지의 생성을 담당.
  - View 는 Controller 에 해당하여, 웹 클라이언트의 요청을 받고 Model 로 넘기거나, Template 에서 생성된 페이지로 응답함.


## API Server
  `웹페이지가 아닌 데이터를 제공하는 서버`

- 응용프로그램을 위한 데이터를 전송하는 서버.
- 공공데이터 또는 지도맵 데이터등을 전송하는 서버등을 말함.
- 비동기적으로 데이터를 주고 받는 웹사이트 (ajax 등) 에서 페이지를 바로 갱신하는 경우에 사용.
- 누구나 접근할수 있는 경우도 있으나, 대부분의 경우 제공자에게 API_key 를 발급받아, 요청시 키를 파라메터나 헤더에 포함하여 사용함.
- __REST API__ 등의 규칙을 맞추어 제공하면, URL 을 보고서 어떤 데이터를 요청하는지 쉽게 구분할수 있다.
- __Graph QL__ 과 같이 요청시 "쿼리문" 을 포함하여 
