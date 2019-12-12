# 머신러닝 개념

## 비지도 학습
    Generative vs Adversarial
- GAN (생성적 적대신경망) : [위키링크](https://ko.wikipedia.org/wiki/%EC%83%9D%EC%84%B1%EC%A0%81_%EC%A0%81%EB%8C%80_%EC%8B%A0%EA%B2%BD%EB%A7%9D)
    + 생성모델 (Generative Model) : 음성, 사진등
    + 경쟁모델 (Adversarial Model) : 
    [음성합성 링크: Carpedm20](https://carpedm20.github.io/tacotron/)


## 강화학습
    
- 가장 유명한 구글의 구현 (DEEP-Q Learning) [아타리 블록게임](https://www.youtube.com/watch?v=V1eYniJ0Rnk)

## 딥러닝
- 머신러닝의 분야중 하나. 가장 주목 받고 있음.
- 최근에는 기존 머신러닝으로 하던 것들 대부분을 딥러닝으로 대체되어가는 상황 (2019년)

---
## 퍼셉트론
- WX+ b 로, 신경을 토대로 만들어진 이론
- 선형회귀등의 예측모델의 기본단위.


---

## 주로 사용되는 라이브러리
    numpy - 수치연산
    tensorflow - DL (텐서 단위의 API = 저레벨 API)
    keras - DL 의 고레벨 API


---

## 활성화 함수들
    Hidden / Ooutput 별로 구분됨.

### Linear
- 출력그대로 전달.

### RELU
- 0 이하는 0, 1이상은 Linear
- __Gradient Vanishin__ 을 상당히 해결

### Gradient Vanishing : DNN 에서 나타난 문제점.
- 다중 계층에서 발생하는 문제. (AI 2차 겨울의 원인) 
- 입력층과 출력층의 연관성이 사라지는 현상.
- 연속적인 미분등으로 인해서, 입력단으로 갈수록 Weight 가 낮아짐.

### tanh (하이퍼볼릭 탄젠트)
- __HIDDEN LAYER__ 에서 사용.
- feature 값의 범위를 줄여주는 역할. 
- -1 ~ 1 로 출력

### Sigmoid / Softmax 의 차이
- __OUTPUT LAYER__ 에서 사용.
- sigmoid : 2개 사이의 확률을 0~1 사이로 나타냄 (합은 1)
- softmax : 3개 이상간의 확률을 0~1 사이로 나타냄. (합은 1)
- 2개면 sigmoid, 3개 이상의 분류는 softmax
- 공통점 : 합이 1
- 차이점 : 대상의 갯수. 2 vs N 

---

## Lost, Cost 함수
    답을 얼마나 잘 맞추었는가? 를 확인하는 수치.

- MSE : Mean Square Error
    + 최소제곱

![MSE 식](MSE_formula.jpg)

- CEE : Cross Entropy Error
    + 정답을 예측한 확률을 기준으로 오류량 확인.
    + 데이터의 유형에 따라 categorical, binary 등 여러가지 방법 구별.

![CEE 식](CEE_formula.jpg)

---

## Optimizer 최적화
    Weight 를 얼마나 수정 할 것인가? 를 정하는 방법.
    loss 값 * η 을 정하는 계산방법들.
    하이퍼 파라매터를 사람이 직접 설정하여, 최적화 방식 조정가능.
    lr : 러닝레이트. η


### Batch GD : Gradient Descent
- 전체 데이터를 기준으로 LOSS 를 구함.
- __처리 시간__이 길다.
- 답에 가까워질수록 (loss 가 0에 수렴할수록) 느려진다.

### SGD : Stochastic Gradient Descent
- 부분적인 랜덤 데이터를 기준 (10~20%) 으로 LOSS 를 구함.
- 매 에폭때 마다 loss 에 사용되는 데이터가 달라짐.
- BGD 보다는 좀 더 빠르며, Local Minima 에서 나올 확률을 높임.
- GD, SGD 모두 __LR__ 에 크게 좌우 받음.
- 그래도 GD 의 근본적인 단점은 사라지지 않았다. (loss 0에 수렴할수록 느려짐)


#### Local Minima : 옵티마이저에서 발생할수 있는 문제
- GD 과정중에서, 큰 골짜기가 아니라, 작은 골짜기에서 최적화가 끝나는 상황.
[극값위키](https://ko.wikipedia.org/wiki/%EA%B7%B9%EA%B0%92)

### Momentum : 관성
- __이전의 손실기울기값__을 참조하여, 현재의 Loss 화 함께 계산함
- 모멘텀 계수 (감마 γ: 1보다 작은 수) 를 이용해, 이전에 이동하던 속도값의 반영치를 조정.
- Local Minima 문제를 해결.

 ![Momentum 식](momentum.png)
- 하이퍼 파라매터 : lr, 모멘텀계수(γ = 0.9 정도) 


### NAG
    Nesterov Momentum
- 기존 momentum 의 계산을 단축.


### Adagrad : Adaptive Gradient - 적응형 기울기
- 이전에 변동된 __Gradient 의 합__을 사용하여, __Learning Rate 를 변화__ 에 반영
- 기울기 합을 LR 의 분모에 넣고 계산. (식 참조)
- 기울기가 클수록 LR 이 작아지고, 기울기가 작을수록 LR 이 커지는 방식.
- 변화가 적은 Gradient 일때는 적극적으로 값이 변화함.
- 하이퍼 파라매터 : lr, ε

 ![adagrad 식](adagrad.png)
- Gt = 이전에 변동된 gradient 의 합.
- ε = 0 아닌 매우 작은값.


### Adam : Ada]grad + Momentum
- 두가지의 특성을 합친것
- 모멘텀의 일정비율만큼 + Adagrad 의 부분.
- __R-Adam__ 이라는 새로운 알고리즘이 가장 최신의 알고리즘.

 ![adam 식](adam.png)
- β1, β2 를 정함.


### R-ADAM
[논문](https://arxiv.org/abs/1908.03265)
[R ADAM 깃허브](https://github.com/LiyuanLucasLiu/RAdam)

---

## 딥러닝 실습

### CNN 에서 피처 뽑기
    Channel, Filter, Feature map, Padding

- Channel : 컬러 등
- Filter : 합성곱을 구할 영역의 크기 및 값들.
    + 각 값들마다 곱하고, 합침.
- Feature Map

- **Inception v3** (구글넷 머신러닝) 의 구현방식.


### RNN
    
- __Recursive__ Neural Network
- 연속적인 입력의 형태 (글의 문장) 을 학습시키는 방법
- __시계열 데이터__등 연속적 데이터 분석에 적합

>H = F(H', x)
- H : 새로운 상태
- F : 파라매터가 포함된 함수
- H' : 이전의 상태
- x : 이번에 입력될 벡터

이러한 방식으로, 재귀식으로 직렬데이터를 학습.

#### RNN 응용 분야
1. 주식시장 또는 집값변화등
2. 대화봇 (자동 응답 또는 일상적인 답변 부분)
3. 문서 분류 (특허관련)
4. 번역

#### Rnn 네트워크 방식
- 1 to 1
- n to 1
- n to n

#### RNN 모델의 다양한 유형과 특징
- LSTM : H' 에 반영되는 이전 데이터를 여러개 쓰는것.
- GRU : LSTM 의 간소화 버젼 (한국에서 만듬.)



## 딥러닝의 성능을 늘리는법? (CNN)

- 층을 늘리자!! 더.많.이
    + 파라매터가 너무 늘어나서 __OVER FITTING__

- Sparsely Connected
    + 현 레이어에서 유사한 것들은 skip 하여, 다음 계층의 계산에서 생략.
    + 그래    도 성능이 좋지 않았다.

- 레이어 튜닝 (Googlenet)
    + 1x1 레이어를 통해 깊이를 만듬.
    + 데이터를 다양한 크기의 필터를 사용하여 피처를 확인하는 방법.
    + 그리고 3x3 필터 2개가 5x5 필터를 사용하는것보다 연산량이 적어서, v3 버젼부터는 3x3 필터를 2개 사용하는 것으로 바뀜


## Batch Normalization
    모델을 정규화 하는 최적화 기법.

- 데이터 분포를 늘리는 것 ?
- 공변환 (?)
- 레이어 단위의 출력들을 정규화 하는 것?
    + Conv2D (합성곱계층) 에서 각 출력값들을 정규화.
    + BatchNormalization


---

## R-CNN
- 딥러닝을 이용한 머신러닝기능을 혼합한 기능 (Classification 및 Detection)
- 입력데이터의 Image 에 사람이 직접 boxing - labeling 
- ensanble 을 이용한 기능보다 향상된 기법

- __R-CNN 의 과정__
    1. Selective Search 로 Object 후보군(Proposal) 검출(2000개)
    2. 후보군이 있는것으로 보이면, proposal 에 박싱
    3. proposal 을 CNN 에 통과시켜 Feature map 벡터 추출
    4. 해당 피처맵으로 분류기에서 분류
    5. 박싱에 라벨 분류한 결과를 부착, 

- 한계
    1. 너무 오래걸림
    2. 리사이즈의 왜곡 손실
    3. 3가지의 모델 학습 필요


## Fast R-CNN



## YOLO 
    You Only Look Once
    이미지 DNN 프레임워크.

- 하나의 영상에서 여러가지 객체를 빠르게 검출.
- RNN 보다 훨씬 빠르나, 작은 물체등의 검출이 어려운 등의 단점존재
- 적절한 수준에서 검출수준이 매우 높음.
- IOU 라고 하는, 검출범위를 Loss 로 계산.
- IOU : 오브젝트와 바운딩 박스간의 물체 확률.

- 기반 모델 : GoogLeNet 에서 영감을 받아 설계.
    + Inception 모델 대신 1*1 필터.
    + 24개의 레이어
    + FAST YOLO => 9개 레이어 사용. 

<!-- - FC : Fully Connected (Layer) -->
    











