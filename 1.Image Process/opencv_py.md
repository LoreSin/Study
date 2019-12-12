# 파이썬에서 opencv 다루기
    설치방법 : pip install opencv-python
    아나콘다 : conda install -c conda-forge opencv
    기본적으로 opencv 영상을 다룰때는 numpy 라이브러리를 함께 사용한다.

- [한글 튜토리얼](https://opencv-python.readthedocs.io/en/latest/index.html)
- [영어 튜토리얼](https://opencv-python-tutroals.readthedocs.io/en/latest/)

## 기본 코드
    사진, 또는 영상(파일 또는 캠) 다루기
    색상 변경

```py
import cv2 # 라이브러리 임포트 방법.
import numpy as np # 파일이미지는 넘파이의 어레이 방법으로 접근

image = cv2.imread('sample.jpg', cv2.IMREAD_COLOR) # 컬러로 불러오기
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY) # 컬러 to 그레이
background = np.array((100,100,3), dtype=np.uint8) # 3채널 100,100 크기이미지 생성
background += 255  # 모든 하소에 255 더해줌. 넘파이어레이의 브로드 캐스팅 기능.
cv2.imshow('image', image) # 윈도우 이름에 띄우기
key = cv2.waitKey(0) # n 초 단위마다 입력. 0은 정지 상태로 1회 입력을 기다림.
cv2.destroyAllWindows() # 켜진창 모두 파괴
```


## 도형 그리기
    선, 사각형, 원, 타원, 문자


#### 주요 함수들
- cv2.line, cv2.**rectange**, cv2.**circle**, cv2.ellipse, cv2.polylines, cv2.**putText**
- 각 함수마다 요구되는 것은 비슷하나, 파라매터에 주의 



```py
pt1, pt2 = (10,10), (20,20)
RED = (0,0,2 55) # 통상 RGB 로 부르지만, cv2 에서는 역순으로 취급.
CYAN = (255, 255, 0)
cv2.line(image, pt1, pt2, CYAN) # 이미지에 선 그리기
cv2.rectangle(image, pt1, pt2, CYAN) # 이미지에 사각형 그리기
cv2.circle(image, py1, radius, RED)
cv2.polylines(image, [[py1, pt2, (100,100), (100, 50)]], True, (0, 255, 255))
cv2.putText(image, '문자', (0, 100), cv2.FONT_HERSHEY_SIMPLEX, 20, (0,0,0))

```



## GUI 조작
    마우스 키보드 입력, 트랙바
    각 요소마다 처리하는 방법이 다르다.


```py
key = cv2.waitKey(10) # 키 값을 아스키값으로 변환하여 반환
# key = cv2.waitKeyEx(10) # 확장된 키보드값을 반환. (ex insert, 방향키등이 포함)
print(key)
if key == 27:break # esc 키를 눌러 종료함. 값들은 고유의 ASCII 코드값 또는 문자
# 키값을 알고 싶다면, print(key) 등으로 확인하는 방법도 가능.

cv2.setMouseCallback('window', func, [param])
# 'window' 는 해당 윈도우에 마우스콜백을 정해준다는 의미.
# func 는 마우스를 움직일때, 실행하고자 하는 함수.
# [param] 은 별도로 추가 인자를 넣고자 할때 사용.

cv2.createTrackbar('track', 'window', 0, 255, changeFunc) # 트랙바 초기 0,  최대 255 로 생성. 
value = cv2.getTrackbarPos('track', 'window') # 해당 트랙바의 값을 가져옴
cv2.setTrackbarPos('track', 'window', 100) # 해당 트랙바의 값을 설정

# 트랙바를 움직이면, changeFunc 로 하나의 인자(해당 값) 을 넘기며 수행.
# window 부분을 class 로 구현하면, 쉽게 클래스를 통해 컨트롤이 쉬워질것 같다.

```


## 이미지 기본 사용법
    픽셀접근, ROI (Region of Interest), merge

```py
image = imread('image.jpg')
image[10,20] # 특정 픽셀의 값을 접근.
roi = image[10:40,20:50] # 특정 사진의 범위에 해당하는 픽셀값을 불러옴.
roi += 10  # 해당 값을 연산등을 하여 처리도 가능.
b,g,r= cv2.split(image)  # 채널별로 이미지를 분리
image = cv2.merge((r,g,b)) # 채널을 합친 이미지화
```

## 이미지 기본연산
    add, addWeighted 등.(합치기, 가중치 합치기)
```py
a, b = np.uint8([250]), np.uint8([10])
cv2.add(a, b)  # 250 + 10 = 260 이지만, 자료형의 범위에 맞게 255로 채워줌. 
a + b  #  250 + 10 = 260 이지만, 260%256 = 4 로 짤려나간 값이 남음.
dst = cv2.addWeighted(img1, 0,7, img2, 0,3, 0) # 가중치를 각 이미지에 둔다.
```

## 필터
    이미지 필터등을 이용한 처리




# 파이썬에서 opencv 다루기
    설치방법 : pip install opencv-python
    아나콘다 : conda install -c conda-forge opencv
    기본적으로 opencv 영상을 다룰때는 numpy 라이브러리를 함께 사용한다.


## 기본 코드
    사진, 또는 영상(파일 또는 캠) 다루기
    색상 변경

```py
import cv2 # 라이브러리 임포트 방법.
import numpy as np # 파일이미지는 넘파이의 어레이 방법으로 접근


image = cv2.imread('sample.jpg', cv2.IMREAD_COLOR) # 컬러로 불러오기
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY) # 컬러 to 그레이
background = np.array((100,100,3), dtype=np.uint8) # 3채널 100,100 크기이미지 생성
background += 255  # 모든 하소에 255 더해줌. 넘파이어레이의 브로드 캐스팅 기능.
cv2.imshow('image', image) # 윈도우 이름에 띄우기
key = cv2.waitKey(0) # n 초 단위마다 입력. 0은 정지 상태로 1회 입력을 기다림.
cv2.destroyAllWindows() # 켜진창 모두 파괴
```


## 도형 그리기
    선, 사각형, 원, 타원, 문자


#### 주요 함수들
- cv2.line, cv2.**rectange**, cv2.**circle**, cv2.ellipse, cv2.polylines, cv2.**putText**
- 각 함수마다 요구되는 것은 비슷하나, 파라매터에 주의 



```py
pt1, pt2 = (10,10), (20,20)
RED = (0,0,2 55) # 통상 RGB 로 부르지만, cv2 에서는 역순으로 취급.
CYAN = (255, 255, 0)
cv2.line(image, pt1, pt2, CYAN) # 이미지에 선 그리기
cv2.rectangle(image, pt1, pt2, CYAN) # 이미지에 사각형 그리기
cv2.circle(image, py1, radius, RED)
cv2.polylines(image, [[py1, pt2, (100,100), (100, 50)]], True, (0, 255, 255))
cv2.putText(image, '문자', (0, 100), cv2.FONT_HERSHEY_SIMPLEX, 20, (0,0,0))

```



## GUI 조작
    setMouseCallback, createTrackbar, waitKey
    마우스 키보드 입력, 트랙바
    각 요소마다 처리하는 방법이 다르다.


```py
key = cv2.waitKey(10) # 키 값을 아스키값으로 변환하여 반환
        # key = cv2.waitKeyEx(10) # 확장된 키보드값을 반환. (ex insert, 방향키등이 포함)
print(key)
if key == 27:break # esc 키를 눌러 종료함. 값들은 고유의 ASCII 코드값 또는 문자
# 키값을 알고 싶다면, print(key) 등으로 확인하는 방법도 가능.

cv2.setMouseCallback('window', func, [param])
# 'window' 는 해당 윈도우에 마우스콜백을 정해준다는 의미.
# func 는 마우스를 움직일때, 실행하고자 하는 함수.
# [param] 은 별도로 추가 인자를 넣고자 할때 사용.

cv2.createTrackbar('track', 'window', 0, 255, changeFunc) # 트랙바 초기 0,  최대 255 로 생성. 
value = cv2.getTrackbarPos('track', 'window') # 해당 트랙바의 값을 가져옴
cv2.setTrackbarPos('track', 'window', 100) # 해당 트랙바의 값을 설정

# 트랙바를 움직이면, changeFunc 로 하나의 인자(해당 값) 을 넘기며 수행.
# window 부분을 class 로 구현하면, 쉽게 클래스를 통해 컨트롤이 쉬워질것 같다.

```


## 이미지 기본 사용법
    픽셀접근, ROI (Region of Interest), merge

```py
image = imread('image.jpg')
image[10,20] # 특정 픽셀의 값을 접근.
roi = image[10:40,20:50] # 특정 사진의 범위에 해당하는 픽셀값을 불러옴.
roi += 10  # 해당 값을 연산등을 하여 처리도 가능.
b,g,r= cv2.split(image)  # 채널별로 이미지를 분리
image = cv2.merge((r,g,b)) # 채널을 합친 이미지화
```

## 이미지 기본연산
    add, addWeighted 등.(합치기, 가중치 합치기)
    bitwise_or, bitwise_and, bitwise_not 등의 비트연산 마스크 또는 영역추출등 사용.
```py
a, b = np.uint8([250]), np.uint8([10])
cv2.add(a, b)  # 250 + 10 = 260 이지만, 자료형의 범위에 맞게 255로 채워줌. 
a + b  #  250 + 10 = 260 이지만, 260%256 = 4 로 짤려나간 값이 남음.
dst = cv2.addWeighted(img1, 0,7, img2, 0,3, 0) # 가중치를 각 이미지에 둔다.


# 비트연산
img1 = cv2.imread('logo.png')
img2 = cv2.imread('lenna.png')
rows, cols, channels = img1.shape
roi = img2[0:rows, 0:cols]
img2gray = cv2.cvtColor(img1, cv2.cvtColor(cv2.COLOR_BGR2GRAY))
ret, mask = cv2.threshold(img2gray, 10, 255, cv2.THRESH_BINARY) # 바이너리 마스크 생성
mask_inv = cv2.bitwise_not(mask) # 바이너리로 된 마스크 반전.

img1_fg = cv2.bitwise_and(img1, img1, mask=mask)
img2_fg = cv2.bitwise_and(roi, roi, mask=mask_inv)
dst = cv2.add(img1_fg, img2_fg)
img2[0:rows, 0:cols] = dst  # 영상 대입하여 img1 을 img2 에 붙여 합침.



```

## 이미지 처리
    cvtColor, inrange
    Binary, Grayscale, RGB, HSV 별 차이.


- Binary : 2진화된 데이터. (흑백)
- Grayscale : 음영데이터. 1채널 컬러.
- RGB : red, green, blue 의 3채널 컬러
- HSV : Hue, Saturation, Value 로 표현되는 3채널 컬러.
    + H 는 색상. 0~179 의 값을 사용. (0: red, 90 : green, 179: blue)
    + S 는 채도. 색상이 얼마나 진한가 흐린가. 
    + V 는 명도. 얼마나 밝고 어두운가. (밝기)
    + **특정색상을 검출**하는데는 HSV 가 더 좋다. 

```py
hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV) # BGR 을 HSV 형태로 변환.

lower_blue = np.array([110, 50, 50])
upper_blue = np.array([130, 255, 255])

#이미지에서 blue영역
mask = cv2.inRange(hsv, lower_blue, upper_blue)

#bit연산자를 통해서 blue영역만 남김.
res = cv2.bitwise_and(frame, frame, mask = mask)
```

#### 임계처리
    threshold, adaptiveThreshold
    바이너리화 하거나, 특정 색상구간을 통과/차단.
    그레이스케일(1채널)로 조정된 영상을 사용한다.
    RGB 의 특정생상만을 사용하기도 한다.

```py
ret, thresh1 = cv2.threshold(img,127,255, cv2.THRESH_BINARY) # 2진화
ret, thresh2 = cv2.threshold(img,127,255, cv2.THRESH_BINARY_INV) # 2진화 반전
ret, thresh3 = cv2.threshold(img,127,255, cv2.THRESH_TRUNC) # 임계점 구간내 1로
ret, thresh4 = cv2.threshold(img,127,255, cv2.THRESH_TOZERO) # 임계점 구간외는 0으로
ret, thresh5 = cv2.threshold(img,127,255, cv2.THRESH_TOZERO_INV) # 임계점 구간내를 0으로

th2 = adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_MEAN_C, cv2.THRESH_BINARY, 15,2)
# 픽셀값을 주변의 평균으로 결정.
th3 = adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 15,2)
# 픽셀값을 가우시안평균으로 결정

ret4, th4 = cv2.threshold(img, 0, 255, cv2.THRESH_BINARY+cv2.THRESH_OTSU)
# Otsu 를 이용한 방법. 히스토그램을 이용해 자동으로 임계값을 설정함.

```

## 기하학적 변형
    Scaling, Translation, Rotation : 확대축소, 이동, 회전
    Affine Transform : 수평수직변형
    PerspectiveTransform : 원근변환 

```py
# Scaling
shrink = cv2.resize(img, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA) # 0.5배 축소
zoom1 = cv2.resize(img, (width*2, height*2), interpolation=cv2.INTER_CUBIC) # 직접지정
zoom2 = cv2.resize(img, None, fx=2, fy=2, interpolation=cv2.INTER_CUBIC)  # 2배수확대

# translation 
rows, cols = img.shape
M = np.float32([[1,0,10],[0,1,20]]) # 이동행렬 생성. x = 10, y = 20 이동
cv2.warpAffine(img, M, (cols, rows))

cv2.getRotationMatrix2D((cols/2, rows/2), 90, 0.5)  # 중심점에서 90도 회전 & 0.5 로 축소.

pts1 = np.float32([[200,100],[400,100],[200,200]])
pts2 = np.float32([[200,300],[400,200],[200,400]])
M = cv2.getAffineTransform(pts1, pts2)  # 변형행렬공식 생성 3점을 기준으로 평행비틀기
dst = cv2.warpAffine(img, M, (cols, rows))

# pts1:포인트를 좌상-좌하-우상-우하점을 찍음. 소실점을 계산하는 포인트.
# pts2:포인트를 좌상-좌하-우상-우하점을 찍음. 원본에서 원근사진에서 평면화 처럼 해줌.
# pts1 의 각 포인트가, pts2 의 각 포인트를 기준으로 그림을 출력
pts1 = np.float32([[504,1003],[243,1525],[1000,1000],[1280,1685]]) 
pts2 = np.float32([[10,10],[10,1000],[1000,10],[1000,1000]])
M = cv2.getPerspectiveTransform(pts1, pts2)
dst = cv2.warpPerspective(img, M, (1100, 1100))
```





