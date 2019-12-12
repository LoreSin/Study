# YOLO 실습 및 정리
    실습에는 욜로를 케라스로 변경한 (학습된 자료들만 사용) 버젼을 사용함.

- [공식사이트](https://pjreddie.com/darknet/yolo/)
- [욜로3 케라스 깃허브](https://github.com/qqwweee/keras-yolo3)

## 특징

- 매우 빠른 + 여러가지를 검출하는 방법을 논문으로 하여 구현된 모델
- 하나의 영상에서 여러가지 객체를 빠르게 검출.
- RNN 보다 훨씬 빠르나, 작은 물체등의 검출이 어려운 등의 단점존재
- 적절한 수준에서 검출수준이 매우 높음.
- IOU 를 사용하여 loss 계산에 쓰임. 
- 기반 모델 : (CNN 유형)
    + FAST YOLO => 9개의 Conv 사용. 


## 라벨링 하기 (데이터셋 준비)

    LabelImg 라는 이미지의 라벨 xml 을 만들어내는 라이브러리

- 설치 명령어 [pip install labelimg]
- 사용 명령어 [labelimg]

[이미지의 구역라벨링 하는 프로그램](https://github.com/tzutalin/labelImg)

- 최대한 다양한 + 많은 종류의 라벨을 사용하여, 데이터셋을 구축함.



## 라벨링 된 xml 파일의 데이터화

- yolo.weight 파일을 h5 로 컨버팅 (yolo v3 에서 미리 학습된 W 값)
[python convert.py yolov3.cfg yolov3.weight model_data/yolo.h5]




## 욜로v3 모델을 이용한 검출.  (80가지의 검출)
- 이미지 검출 : [python execute_code.py --image 파일명]
- 비디오 검출 : [python execute_code.py 입력파일명 출력파일명]

## 직접 학습 시켜본 데이터
- (욜로-커스텀 모델)[https://github.com/LoreSin/yolo_keras_custom]
