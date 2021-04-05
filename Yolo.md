Yolo는 이미지 내의 bounding box와 class probability를 한번 회귀 문제로 생각하여, 이미지를 네트워크에 한번 통과시키는 것으로 object에 종류와 위치를 추측한다. 
![image](https://user-images.githubusercontent.com/61510837/113558003-df625d80-9639-11eb-8e1b-0240782d1bdf.png)
장점:
	간단한 처리과정으로 속도가 매우 빠르다. 또한 기존의 다른 real-time detection system들과 비교할 때, 2배 정도 높은 mAP를 보인다.
	Image 전체를 한 번에 바라보는 방식으로 class에 대한 맥락적 이해도가 높다. 이 때문에 낮은 background error를 보인다.
	Object에 대한 좀 더 일반화된 특징을 학습한다. 가령 natural image로 학습하고 이를 artwork에 테스트했을 때, 다른 detection system들에 비해 훨씬 높은 성능을 보여준다.
단점:
	상대적으로 낮은 정확도(작은 개체에 대해)를 가지고 있다.
# Overview
1.	Input image를 SxS 그리로 나눈다.
2.	각각의 그리드 셀은 B개의 bounding box와 각 bounding box에 대한 confidence score를 갖는다.
Confidence Score: Pr(Object)∗IOUtruthpred
3.	각각의 그리드 셀은 C개의 conditional class probability를 갖는다.
Conditional Class Probability: Pr(Classi|Object)
4.	각각의 bounding box는 x, y, w, h, confidence로 구성된다.
Test때 conditional class prbability와 bounding box의 confidence score를 곱하여 class-specific confidence score를 얻는다.
ClassSpecificConfidenceScore=ConditionalClassProbability∗ConfidenceScore=Pr(Classi|Object)∗Pr(Object)∗IOUtruthpred=Pr(Classi)∗IOUtruthpred
# Network Design
Yolo의 네트워크 아키텍쳐는 GooLeNet을 기반으로 한다. 다만 convolution layer를 3x3으로 한정하였으며 auxiliary classifier가 없다.
![image](https://user-images.githubusercontent.com/61510837/113558051-f608b480-9639-11eb-9475-061053d605a0.png)
# Inference Process
![image](https://user-images.githubusercontent.com/61510837/113558072-fdc85900-9639-11eb-9ed2-c04f48d2f976.png)
만약 그리드가 7x7이라면 49개의 그리드 셀이 된다. 그리드당 2개의 bounding box를 예측하고, 박스는 x, y, w, h, confidence로 5개의 정보가 있다. 나머지는 출력 class에 대한 conditional class probability로 총 출력 텐서는 10+Class 가 된다.
또한, bounding box는 2개의 예측으로 총 49개의 그리드 이므로 총 98개의 예측박스가 생성된다.
![image](https://user-images.githubusercontent.com/61510837/113558090-03be3a00-963a-11eb-86cb-595cd7148df9.png)
# Loss Function
머신러닝에서 가장 중요한 로스 계산이다.
![image](https://user-images.githubusercontent.com/61510837/113558123-0de03880-963a-11eb-8b51-19f002e1113e.png)
(1)	Object가 존재하는 grid cell i의 predictor bounding box j에 대해, x와 y의 loss를 계산.
(2)	Object가 존재하는 grid cell i의 predictor bounding box j에 대해, w와 h의 loss를 계산. 큰 box에 대해서는 small deviation을 반영하기 위해 제곱근을 취한 후, sum-squared error를 한다.(크기가 커지면 w와 h에 변동에 더 강인 해진다)
(3)	Object가 존재하는 grid cell i의 predictor bounding box j에 대해, confidence score의 loss를 계산.
(4)	Object가 존재하지 않는 grid cell i의 bounding box j에 대해, confidence score의 loss를 계산.
  (5) Object가 존재하는 grid cell i에 대해, conditional class probability의 loss 계산.
λcoordλcoord: coordinates(x,y,w,h)에 대한 loss와 다른 loss들과의 균형을 위한 balancing parameter.
λnoobjλnoobj: obj가 있는 box와 없는 box간에 균형을 위한 balancing parameter. (일반적으로 image내에는 obj가 있는 cell보다는 obj가 없는 cell이 훨씬 많으므로)
사용하는 활성화 함수는 leaky relu이다.
# Cfg
![image](https://user-images.githubusercontent.com/61510837/113558181-27818000-963a-11eb-86f4-26131fe5db3e.png)
1.	#test는 학습이 아닌 demo시 사용하는 설정으로, 학습과 다르게 이미지 한 장씩 regression 되므로 batch와 subdivisions를 늘려 gpu에 메모리에 부하를 줄 필요가 없다. 
2.	Batch는 이미지를 몇 개로 나누어 묶음으로 학습하느냐인데, 위 사진에 경우 1회 학습에 64개의 데이터를 사용하겠다는 것이다.
3.	Subdivision은 이러한 batch를 몇 개로 나누어 gpu에 보내냐는 것으로 보통 gpu 메모리 부족일 때 조절하도록 한다. 그만큼 학습 속도는 줄어든다.
4.	Width, height는 학습 또는 testing시 resizing되는 이미지 크기다.
5.	Max_batches는 train_detector함수에서 종료 시점과 608 해상도로 고정을 위해 쓰이는 최대 학습 횟수가 될 것이다. 정확하게는 설정한 batch*학습 횟수가 max_batch를 넘지 말아야 한다.
6.	아래에는 이미지를 증강시키는 옵션이 있다. Angle은 사진에 각도를, saturation은 채도를, exposure은 노출 수준을, flip은 좌, 우 반전을 허용하여 데이터가 여러 경우로 증폭되게 한다.
7.	Learning rate는 역전파시 loss에 맞춰 가중치를 조정하는데 있어서 얼마만큼 조정을 할 것인지에 대한 크기 조절이다.
#
![image](https://user-images.githubusercontent.com/61510837/113558205-30725180-963a-11eb-85e8-e3d61097eda4.png)
1.	컨볼루션 레이어로 batch_normalize와 padding을 위한 옵션이 있다. 활성화 함수는 leaky relu를 사용하며 3x3 커널을 사용한다.
2.	Filters=32는 32 채널에 3x3 convolutional 커널을 사용하겠다는 것이다.
3.	Stride는 컨볼루션 연산시 얼만큼 이동을 하면서 연산 할 것인지에 대한 옵션이다.
#
![image](https://user-images.githubusercontent.com/61510837/113558220-3700c900-963a-11eb-81fc-42e9d270dff1.png)
1.	Shortcut은 restnet에서 나온 skip connection과 유사한 기능으로 from=-3은 3번째 전 layer의 값을 더해주겠다는 것이다.
#
![image](https://user-images.githubusercontent.com/61510837/113558241-41bb5e00-963a-11eb-94a9-147b701174bc.png)
1.	Yolo는 feature extracting 후 박스와 class를 구분하는 layer로 mask는 anchors중 어떤 것을 사용할 것인지 여부이다.
2.	Anchors는 미리 지정한 box로 사전 정의한 box를 조절하는 식으로 위치를 추정한다.
3.	Classes는 클래스의 개수이다.
# Yolo 실행 환경
![image](https://user-images.githubusercontent.com/61510837/113558269-4e3fb680-963a-11eb-9b7f-d245351975f6.png)
# 설치 방법(for Ubuntu18.04)
1.	본인이 GPU가 있는 경우 gpu에 맞는 cuda와 cudnn 및 toolkit을 설치해준다.
2.	Opencv 3.2 또는 3.4를 설치하고 build한다.
3.	Git clone git@github.com:pjreddie/darknet.git 다음과 같은 명령을 터미널에 입력하여 darknet 패키지를 받는다.

![image](https://user-images.githubusercontent.com/61510837/113558299-5dbeff80-963a-11eb-940d-7e0ed93d8f65.png)

4.	다음과 같이 Makefile을 컴퓨터 조건에 따라 맞추어 주고 make한다.
- Gpu를 쓰는 경우 1로 표기
- OPENCV를 쓰는 경우 1로 표기
5. wget https://pjreddie.com/media/files/yolo.weights 해당 명령어로 실험 가중치 파일을 받는다.
6. ./darknet detect cfg/yolo.cfg yolo.weights data/dog.jpg 해당 명령문으로 테스트를 해본다.


