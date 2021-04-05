# BBD 100K: A Large-scale Diverse Driving Video Database
![image](https://user-images.githubusercontent.com/61510837/113557061-61518700-9638-11eb-9da3-8eb52b94e7b1.png)
UC 버클리 인공 지능 연구 실험실(BAIR)에서 공개한 운전 데이터베이스이다. 거친 주행 환경 구현, GPS정보, IMU 데이터 및 타임 스탬프가 포함되어 있다. 녹화된 비디오는 비가 오는 날씨, 흐린 날씨, 맑은 날씨, 안개와 같은 다양한 날씨 조건이 기록되어 있다. 데이터 세트는 낮과 밤이 적절한 비율로 기록된다
# IMFORMATION: 
영상길이: 40초
Resolution: 720p
Fps: 30
총 100,000개 비디오 데이터
이미지에 쉽게 주석 처리하기 위해, 수직 차선은 적색, 평행 차선은 청색으로 되어있다. 
![image](https://user-images.githubusercontent.com/61510837/113557134-7cbc9200-9638-11eb-93fa-7cbde4f08c55.png)
버스, 신호등, 교통 표지, 자전거, 트럭, 오토바이, 라이더, 자동차, 기차로 분류되며 10만개의 영상에 2D bounding box가 포함되어 있다. ![image](https://user-images.githubusercontent.com/61510837/113557159-87772700-9638-11eb-9d0d-27d9f1d41713.png)
뿐만 아니라, 도로 및 포장 도로의 보행자 탐지를 위해 85000개가 넘는 보행자 인스턴스가 있다.
# Recommended Task
1.	도로 객체 감지
2.	인스턴스 세그먼테이션
3.	운전 가능 지역
4.	차선 구분
5.	시메틱 세그먼테이션
# Using data
https://bdd-data.berkeley.edu/index.html 방문하여 회원 가입 후 BDD100k를 다운 받을 수 있다.![image](https://user-images.githubusercontent.com/61510837/113557226-a4135f00-9638-11eb-8e19-3666d9f761c7.png)
# Example
![image](https://user-images.githubusercontent.com/61510837/113557250-ab3a6d00-9638-11eb-882d-e700642ab6a8.png) ![image](https://user-images.githubusercontent.com/61510837/113557254-ad9cc700-9638-11eb-9774-fa864712aef5.png)
라벨은 json 파일 포맷이며, category, attributes, bounding box로 이루어져 있다.
![image](https://user-images.githubusercontent.com/61510837/113557264-b2fa1180-9638-11eb-91b3-3308680f812d.png)
인스턴스 세그먼테이션은 7000개 훈련용 데이터셋과 1000개의 검증용 데이터셋을 제공한다.

# KITTI
자율 주행 플랫폼 Annieway를 사용한 데이터셋으로 차량에는 벨로다인 라이다와 GPS 및 높은 해상도를 가진 컬러 및 흑백 사진이 있다. 중형 도시인 Karlsruhe에 주변을 주행하면서 가지고 온 데이터로 마을과 고속도로에 정보가 있다. 이미지당 최대 15대의 자동차와 30명의 보행자가 있다. 
# SENSOR
GPS: OXTS RT 3003
Laserscanner: Velodyne HDL-64E
Grayscale cameras: Point Grey Flea2 (FL2-14S3M-C)
Color cameras: Point Grey Flea2 (FL2-14S3C-C)
Varifocal lenses: Edmund Optics NT59-917
# Using data
http://www.cvlibs.net/datasets/kitti/index.php 에 접속하여 아래에 category 중 원하는 데이터를 선택해 본인 이메일로 파일을 받는다.
Stereo Evaluation 2015 데이터 기준 training set은 각 카메라에 대한 상이 데이터와flow 데이터, 및 각 카메라에 들어온 rgb이미지 파일과 visualization_flow 가 있습니다. 예시 데이터를 하나씩 보여드리겠습니다.
# BBD 100K: A Large-scale Diverse Driving Video Database
![image](https://user-images.githubusercontent.com/61510837/113557061-61518700-9638-11eb-9da3-8eb52b94e7b1.png)
UC 버클리 인공 지능 연구 실험실(BAIR)에서 공개한 운전 데이터베이스이다. 거친 주행 환경 구현, GPS정보, IMU 데이터 및 타임 스탬프가 포함되어 있다. 녹화된 비디오는 비가 오는 날씨, 흐린 날씨, 맑은 날씨, 안개와 같은 다양한 날씨 조건이 기록되어 있다. 데이터 세트는 낮과 밤이 적절한 비율로 기록된다
# IMFORMATION: 
영상길이: 40초
Resolution: 720p
Fps: 30
총 100,000개 비디오 데이터
이미지에 쉽게 주석 처리하기 위해, 수직 차선은 적색, 평행 차선은 청색으로 되어있다. 
![image](https://user-images.githubusercontent.com/61510837/113557134-7cbc9200-9638-11eb-93fa-7cbde4f08c55.png)
버스, 신호등, 교통 표지, 자전거, 트럭, 오토바이, 라이더, 자동차, 기차로 분류되며 10만개의 영상에 2D bounding box가 포함되어 있다. ![image](https://user-images.githubusercontent.com/61510837/113557159-87772700-9638-11eb-9d0d-27d9f1d41713.png)
뿐만 아니라, 도로 및 포장 도로의 보행자 탐지를 위해 85000개가 넘는 보행자 인스턴스가 있다.
# Recommended Task
1.	도로 객체 감지
2.	인스턴스 세그먼테이션
3.	운전 가능 지역
4.	차선 구분
5.	시메틱 세그먼테이션
# Using data
https://bdd-data.berkeley.edu/index.html 방문하여 회원 가입 후 BDD100k를 다운 받을 수 있다.![image](https://user-images.githubusercontent.com/61510837/113557226-a4135f00-9638-11eb-8e19-3666d9f761c7.png)
# Example
![image](https://user-images.githubusercontent.com/61510837/113557250-ab3a6d00-9638-11eb-882d-e700642ab6a8.png) ![image](https://user-images.githubusercontent.com/61510837/113557254-ad9cc700-9638-11eb-9774-fa864712aef5.png)
라벨은 json 파일 포맷이며, category, attributes, bounding box로 이루어져 있다.
![image](https://user-images.githubusercontent.com/61510837/113557264-b2fa1180-9638-11eb-91b3-3308680f812d.png)
인스턴스 세그먼테이션은 7000개 훈련용 데이터셋과 1000개의 검증용 데이터셋을 제공한다.

# KITTI
자율 주행 플랫폼 Annieway를 사용한 데이터셋으로 차량에는 벨로다인 라이다와 GPS 및 높은 해상도를 가진 컬러 및 흑백 사진이 있다. 중형 도시인 Karlsruhe에 주변을 주행하면서 가지고 온 데이터로 마을과 고속도로에 정보가 있다. 이미지당 최대 15대의 자동차와 30명의 보행자가 있다. 
# SENSOR
GPS: OXTS RT 3003
Laserscanner: Velodyne HDL-64E
Grayscale cameras: Point Grey Flea2 (FL2-14S3M-C)
Color cameras: Point Grey Flea2 (FL2-14S3C-C)
Varifocal lenses: Edmund Optics NT59-917
# Using data
http://www.cvlibs.net/datasets/kitti/index.php 에 접속하여 아래에 category 중 원하는 데이터를 선택해 본인 이메일로 파일을 받는다.
Stereo Evaluation 2015 데이터 기준 training set은 각 카메라에 대한 상이 데이터와flow 데이터, 및 각 카메라에 들어온 rgb이미지 파일과 visualization_flow 가 있습니다. 예시 데이터를 하나씩 보여드리겠습니다.
![image](https://user-images.githubusercontent.com/61510837/113557648-51867280-9639-11eb-8c43-0e9a03216ea1.png)
![image](https://user-images.githubusercontent.com/61510837/113557663-56e3bd00-9639-11eb-9956-3bd01014bccf.png)
![image](https://user-images.githubusercontent.com/61510837/113557674-5c410780-9639-11eb-9202-c628bf50fa72.png)
![image](https://user-images.githubusercontent.com/61510837/113557686-619e5200-9639-11eb-9a99-65f2955f0fa3.png)
OCC는 occluded region NOC는 non occluded region으로 가려진 픽셀을 포함 할 것인지 아닌지를 구분한다. 이 데이터로 스트레오 카메라 기반에 feature & tracking을 하는데 사용할 수 있다.

# WAYMO Open DATAset: 
Waymo Open Dataset은 2019년 8월에 고해상도 센서 데이터와 1950개의 세그먼트에 대한 레이블로 구성된 인식 데이터 세트로 처음 출시되었다. 2021년 3월 103354개의 세그먼트로 확장, 객체 궤적과 해당 3D지도로 구성된 모션 데이터 세트도 포함되었다.
![image](https://user-images.githubusercontent.com/61510837/113557789-8abee280-9639-11eb-9824-5f1d92e14114.png)
![image](https://user-images.githubusercontent.com/61510837/113557799-8d213c80-9639-11eb-9af0-aabed41c19ee.png)
10Hz(390000 프레임)로 수집되어 총 1950개의 세그먼트로 구성되었다.
	센서 데이터
중거리 라이더 1개
단거리 라이더 4개
카메라 5대 (전면 및 측면)
	레이블 데이터
차량, 보행자 자전거, 표지판
1200개 세그먼트 lidar 라벨
추적ID가 있는 12.6M 3D
1000개 세그먼트 카메라 라벨
추적ID 11.8M 2D 상자 레이블
	지역
San Francisco, Mountain, Los Angeles, Detroit, Seattle, Phoenix

라이다 데이터는 다음과 같은 특성을 따릅니다.
1.	레이블이 지정되지 않은 영역 NLZ가 포함될 수 있다.
2.	X축으로 회전하는 각도 ([-pi, pi]로 정규화 되었다)
3.	첫 입력 때 2번에 레이저 펄스를 수신한다.

# 데이터의 취득 방법
![image](https://user-images.githubusercontent.com/61510837/113557831-9b6f5880-9639-11eb-8677-7ba1babd234b.png)
https://github.com/waymo-research/waymo-open-dataset.git 에서 데이터를 load
![image](https://user-images.githubusercontent.com/61510837/113557845-a2966680-9639-11eb-84d8-ce52e9cd5106.png)
다음과 같이 Frame화 시킨다.
![image](https://user-images.githubusercontent.com/61510837/113557872-aaeea180-9639-11eb-8fc6-eecdfc5c207f.png)
본 데이터를 통해 라이다 및 카메라를 결합한 센서 퓨전으로 자율주행을 하는데 있어서 라이다가 개체를 잡고 그 개체에 대한 class 정보를 얻기 위해 clustering을 하는데 있어서 groundTruth데이터가 된다.

