# HTML 내용



## 1. 주요참조 링크
- [W3School 태그리스트](https://www.w3schools.com/tags/default.asp)

## 2. 기본 골격

```html
<!DOCTYPE html> <-- 문서의 형태를 선언. html 5 -->
<html> <-- 본문의 영역: html 의 정의 -->
<head> <-- 헤더의 영역: css 또는 javascript 등의 meta 데이터를 정의해 두는 곳 -->
<title>문서 제목 - 웹브라우저 창에서 보이는 이름</title>
</head>
<body> <-- 본문의 영역 -->

<h1>헤더. 통상적으로 </h1>
<p>이 부분은 문단을 나타냄.</p>

</body>
</html>
```

## 3. HTML 5의 레이아웃
  semantic tag 으로 불리는 태그 - 내용을 기준으로 태그화.
 
![HTML5 레이아웃](https://www.w3schools.com/html/img_sem_elements.gif)

- header : 머릿말
- nav : 사이트내 다른 영역의 링크.
- section - 카테고리 등의 영역
- article - 기사 정보.
- aside - 사이드 정보 (사이드바 같은 요소)
- footer - 하단의 끝부분 (사이트 내지는 서비스의 정보 포함)


## 4. Table
  가장 흔하게 쓰는 표를 보여주는 방법.

```html
<table style="width:100%">
  <tr>
    <th>Firstname</th>
    <th>Lastname</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Jill</td>
    <td>Smith</td>
    <td>50</td>
  </tr>
  <tr>
    <td>Eve</td>
    <td>Jackson</td>
    <td>94</td>
  </tr>
</table>

```

- table : 표 시작.
  - tr : Table Row
    - th : Table Header. 첫 tr 에서 컬럼명 선언하는 용도
    - td : Table Data/Cell. 데이터임을 알리는 용도.

