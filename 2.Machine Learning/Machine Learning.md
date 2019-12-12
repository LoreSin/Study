# 머신러닝

##머신러닝 알고리즘들
    - Supervised Learning : 지도학습
        정답이 있는 데이터 (사전입력데이터) 로 학습.
    - Unsupervised Learning
    - Reinforcement learning
    - Deep learning

## Object Detection (Face)

1. Dataset Annotation : Ground True 를 위한 수집
    - 정답있는 데이터 수집 (카메라, 구글, SNS 등)
    - 얼굴위치를 지정하여 잘라내고, 32×32 로 resize (Positive data)
    - 다른 사물과 대상도 32×32 로 resize (Negative data)
    - 두가지의 데이터를 모두 갖고 있어야 하며, 1:3~1:4 정도의 개수를 사용

2. Extract Feature : 특징 추출
    - haar-like : 영역의 픽섹음영차이를 이용한 방법
    - LBP : Local Binary Pattern : 질감표현에도 쓰임. 
    - MCT : Modified Census Transform : 주변픽셀의 밝기비교를 통한 방법.
    - 등의 얼굴 추출 Feature 방법
    - Dataset 을 Feature에 따라 **Feature MAP** 으로 생성.

3. Machine Learning : Classification
    - Logistic Regression
    - adaboost
    - SVM (Support Vector Machine)
    - 위와 같은 알고리즘에 *Feature MAP* 을 사용해 **MODEL** 을 생성

4. Inference : 추론
    - 만들어진 *MODEL*을 이용해, 얼굴을 발견
    - 입력된 모델을 기준으로 **Pyramid Image** 로 만듬. (다양한 크기에서 검출 하는 용도)
    - Pyramid Image 를 순회 하며 MODEL이 검출되는 것을 찾아내는 과정.
    - NMS 등의 방법으로, 검출된 것중 가장 정확할 부분을 출력.

## FACE Detection
    Rapid Object Detection using Boosted Cascade of simple Feature

1. Integral Image : 이미지를 적분하여, 픽셀의 크기합을 구하는 방법.
    - 사진의 부분 정보를 좋은 성능으로 얻는 방법
2. Cascade Adaboost : 복잡한 분포값을 n차 함수(n-1회 꺽인 곡선) 로 계산 하는 대신, 1차 함수 n개 (n개 직선) 를 이용하여 구분하는 방법
    - 부분적 학습 or 실수를 허용하되, 다음 직선에서 해당부분을 더 크게 인식하게 만드는 것.
    - 작은 모델여러개가 겹쳐진 형태로 생각하는게 좋음. (ex 얼굴을 인식하는 작은 단위 여러개를 합친 형태)




######용어들
Bounding Box : 검출코자 하는 오브젝트의 위치 표시
NMS : Non Maximum Suppression : 비최대치 제거 (최대치 생존)
