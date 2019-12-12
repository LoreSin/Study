# CNN 실습 (이미지 구분)


## 이미지 수집 (크롤링)
- zzllrr imager Geek: 구글 확장프로그램
    + 현재 보고 있는 페이지의 사진 다운로드 가능.


## 텐서보드 
    모델의 학습곡선 및 

- tensorboard --logdir=logs/
- 경로명을 적어주면 된다. 바로 하위 경로의 아이템들 까지 플로팅됨


## 구글넷 (Google net)
    구글이 사용한 CNN 모델
- [구글넷 논문](https://www.google.com/search?newwindow=1&sxsrf=ACYBGNQU78tlJB3evYmuSu0g7u61gNyHNg%3A1570521432048&ei=WEGcXafJArWRr7wP8Mis2A4&q=going+deeper+with+convolutions&oq=going+deeper+with+con&gs_l=psy-ab.3.0.0j0i203l7j0j0i203.1524.2694..3333...0.0..0.124.1019.0j9......0....1..gws-wiz.......0i20i263.8qUsutw5RvA)
- Inception 모델이라고 부름. 

- 레이어 튜닝 (Googlenet )
    + 데이터를 다양한 크기의 필터를 사용하여 피처를 확인하는 방법.
    + 그리고 3x3 필터 2개가 5x5 필터를 사용하는것보다 연산량이 적어서, v3 버젼부터는 3x3 필터를 2개 사용하는 것으로 사용



### 논문 찾는 방법

- 구글에서 [paperswithcode sota] 검색. 현재 권위있는 (코드관련) 논문이 나옴.
- 딥러닝 분야별 논문 및 코드를 찾아보기 쉽게 되어있음.