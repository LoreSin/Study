# OPENCV
>
OPENCV 는 오픈소스 컴퓨터 비젼 라이브러리를 뜻하며, C++, python 에서 지원한다.

- [Opencv Cookbook 소스](https://github.com/laganiere/OpenCV3Cookbook)
- `Learning Opencv` 라는 opencv 창시자가 만든 책도 존재. (1k page over)
    - 비젼관련 기본부터 나온 책이라고 함. 
    - 제대로 쓰고 배우려고 한다면 가장 좋다고 함. 

## 목차

- [OpenCV 설치](#opencv-install)
- [VS2019](#vs2019)
- [이미지열기및 기본함수](#openimage-and-basic-function)
- [콜백 함수](#callback-function)
- [이미지 생성](#creation-image)


## OpenCV install; 설치하기
>OpenCV 설치
>VisualStudio 2019 에서 사용가능한 VC15 버젼이 있는 opencv4.1.1 버젼을 사용
>윈도우의 경우, 이미 컴파일된 exe 파일 (압축) 을 C:\ 경로에 설치.

## VS2019
>속성관리자에서, 관련 lib 및 include 경로를 추가 해야함
>os 환경의 path 에는 bin 폴더 (바이너리 파일) 을 추가해야 실행 가능한 상태가 됨
>*opencv_world411.lib* 을 윈도우시스템폴더 (sysWOW64) 에 넣어도 된다.

- 프로젝트 속성페이지
    + 포함 디렉토리 (include dir) : 빌드된 opencv의 include 폴더 및 내부 폴더(include/opencv2)
    + 라이브러리 디렉토리 (lib dir) 은 빌드된 opencv의 lib 폴더 의 해당 버젼 (vc15\lib 폴더) 를 추가
    + 링커-종속성 에서는 사용할 라이브러리내의 DLL 파일을 추가 (opencv_world411d.lib)
        * **opencv_world411.lib** 은 이전버젼의 모든 라이브러리를 하나의 파일로 통합시킨 라이브러리. opencv 4.X 버젼에서는 기본으로 이것을 제공. (3.X 이전에는 선택.)


- 프로젝트 속성페이지를 별도로 만들어, 관리하면 나중에 다시 사용할수 있다.
- 디버깅에서 **환경** 경로를 이용하여, 환경변수에 관련 바이너리를 추가하지 않아도 실행 가능하다.
- 
![VS2019 프로젝트에서 디버깅으로 환경설정](환경설정.png)

---

## openImage and basic Function; 이미지 열기 및 기본함수
>opencv4.1.1 c++ 코드 실습 주요 요약 코드

```c++
using namespace cv;
Mat image, inImage, outImage; // 파일 매트릭스 선언 및 정의
image = imread("image/puppy.png", int flags); // 파일열기 flags:색상모드.

imshow("title name", image); // 이미지 창으로 열어보기
waitKey(0); // 일시 정지.없으면, imshow 의 창이 순식간에 꺼짐. 

flip(inImage, outImage, int flipCode); // flipCode : 0 - 상하, 1 - 좌우, -1 - 상하좌우
imwrite("outName.jpg", outImage); // outImage 를 파일명으로 확장자포맷으로 저장.

setMouseCallback("title name", onMouse, userdata); // title name 의 윈도우 onMouse 의 실행.
// onMouse 는 mouseCallback (함수포인터) 와 동일한 형태로 정의된 것이어야 함. 

circle(~~); // 원 그리기 파라매터 참조.
putText(~~); // 텍스트 넣기. 파라매터 참조.

```

---
## CALLBACK Function; 콜백함수
>콜백함수 : 이벤트 또는 인터럽트가 발생될때, 호출될 함수.
>프로그래머는 해당 함수의 파라매터를 동일하게 만들고, 설정필요.

- setMouseCallback 의 파라매터 중 onMouse 는 콜백함수.
- 즉, 프로그래머는 관련 이벤트에 따른 정의를 하고, 사용되는 것.
- 특정 상황 (시간, 인터럽트, 이벤트) 에 "사용자 또는 미리 정의된 이벤트의 액션" 으로 호출


```c++
void onMouse(int event, int x, int y, int flag, void* param){
    Mat* im = reintepret_cast<Mat*>param
    cout << x << ", "<< y << endl;
}
```

## Creation Image; 이미지 생성
>이미지생성 및 변환
>이미지를 초기화하거나, 참조&복사 하는 방법들.

```c++
Mat im1;
Mat im2(240,320, CV_8U);
Mat im3(im2); // 참조
Mat im4 = im2; // 복사
Mat im5 = im1.clone(); // 복제
im4.copyTo(im1); // 복사
im1.convertTo(im3, CV_32F, 1/255.0, 0.0); //변형.
```


## Manipulate Pixel; 픽셀 조정
>화소단위로 픽셀을 접근, 값을 변경하는 법.

``` c++
uchar data[12 * 4] = {
    0x00,0x00,0xFF,0x00,0xFF,0x00,0xFF,0x00,0x00,0xFF,0xFF,0xFF,
    0x00,0x00,0xAA,0x00,0xAA,0x00,0xAA,0x00,0x00,0xAA,0xAA,0xAA,
    0xFF,0x00,0xFF,0x00,0xFF,0xFF,0xFF,0xFF,0x00,0x00,0x00,0x00,
    0x55,0x00,0x55,0x00,0x55,0x55,0x55,0x55,0x00,0x55,0x55,0x55,
}; // 픽셀값 지정

Mat image44(Size(4, 4), CV_8UC3, data); // 픽셀값 적용한 이미지
Mat gray44();
cvtColor(image44, gray44, COLOR_BGR2GRAY); // BGR => 그레이 컬러

image44.at<Vec3d>(y,x) = {255,255,255}; // at 매소드로 픽셀 접근, 흰색적용
uchar b = image44.at<Vec3d>(y,x)[0]; // at 메소드로 픽셀속성접근. 통상적으로 bgr 순

image44.data; // 데이터배열 직접접근
image44.ptr(); // Mat.ptr 로 해당 row 를 접근하는 포인터 반환 ; 0으로 하면 data와 동일
```

## Contrast and Brightness
>픽셀값의 덧셈곱셈 = 산술연산 = 대비밝기 조정.
>덧셈으로 밝고 어두움 (밝기) 
>곱셈으로 대비 강약 (명조)
>TrackBar 로 어느정도 조정가능.

```c++
image.at<uchar>(y,x) = Contrast * value + Brightness // A 는 명조, B 는 밝기 조정
image.at<Vec3d>(y,x)[0~2] = Contrast * value + Brightness // 컬러 픽셀 접근
createTrackbar(~~~) // 트랙바를 해당 창에 생성, 변수를 참조하여 변경하고, 콜백함수 실행
```

