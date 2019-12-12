# 파이썬 3.7
    설치는 여러가지 방법이 있음. 
    1. 공식 사이트에서 받기. 
    2. 아나콘다 패키지 (anaconda)
    3. 파이참 (Pycharm)


#### 1. 파이썬을 사용하는 여러가지 방법

1. 아나콘다 - jupyter notebook, Spyder 등 및 기타 IDE 제공
2. idle (파이썬 기본설치)
3. 파이참. 가상 환경등 여러가지 제공
4. 기타 텍스트에디터

#### 2. 주요 문법
    들여쓰기는 타 언어의 { } 와 같은 구문 구별을 위한 것이다.

```python
a = 10
if a == 10: # 조건식
    print(True)
else:
    print(False)

a = int(input('입력1:'))
b = float(input('입력2:'))
a + b
5 // 2 # 2
5 / 2 # 2.5

a = list(3,4,5,6)
b = tuple(3,4)
[3,4,5,6] * 3 # [3,4,5,6,3,4,5,6,3,4,5,6]

# slice
lists = [1,2,3,4,5,6,7,8,9]
lists[2:4] # [3,4]
lists[2:8:2] # [3,5,7]
lists[5:1:-1] # [6,5,4,3]
lists[5:1:-2] # [6,4]

for x in range(5): # 0~4 반복
    if x == 4: # 3 이면
        break # 탈출
    elif x == 3: # 2 라면
        continue # 다음 실행문 스킵하고, 반복문다음 시작으로.
    print(x)

class Car(object):
    def __init__(self, speed=0): # 파이썬 생성자 문법
        super(Car, self).__init__() # 부모클래스 생성자함수 호출
        self.speed = speed

    def speed_up(self):
        self.speed += 20
        self.speed = 160 if 160 < self.speed else self.speed
        self.print()

    def speed_down(self):
        self.speed -= 20
        self.speed = 0 if self.speed < 0 else self.speed
        self.print()

    def print(self):
        print("현재속도 :", self.speed)

car = Car()
car.speed_up()
car.speed_down()



```





## 주요 사이트 링크
- [파이썬 공식사이트](https://www.python.org)
- [도장.io - 파이썬 강좌사이트](https://dojang.io/course/view.php?id=7)
