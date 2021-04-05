Orb slam은 단안 방식으로 ORB라는 특징점과 기술자를 통해 맵을 생성하고 Localization을 한다. 또한, stereo와 RGB D 경우 깊이 정보를 갖고 있다.

# ORB SLAM2 실행 환경
![image](https://user-images.githubusercontent.com/61510837/113560361-d7a4b800-963d-11eb-9502-91715f9b623f.png)
# 설치 방법(for Ubuntu18.04)
1.	git clone https://github.com/Taeyoung96/Depth-estimation-with-ORB-SLAM2.git 명령문으로 ORB SLAM2 패키지를 받는다.
2.	sudo apt-get install libglew-dev, git clone http://github.com/ktossell/libuvc패키지 내부에서 2개를 설치하여 줍니다.
3.	Libuvc에서 build 후 install 합니다.
4.	다시 본 패키지로 돌아가 Thirdparty 폴더에 git clone https://github.com/stevenlovegrove/Pangolin.git 설치합니다.
5.	설치한 폴더에서 build 후 install 합니다.
6.	마지막으로 패키지 전체적으로 빌드 해줍니다.
7.	./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt ./Examples/Monocular/d435.yaml 명령을 통해 작동을 확인해 봅니다.
