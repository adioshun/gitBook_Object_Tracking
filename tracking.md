## 4. Obstacle tracking

vehicle odometry 정보 추가적으로 활용

연속적으로 얻어지는 인식 결과를 바탕으로 이러한 오탐을 줄일 수 있는데, 이룰 추적기법(Tracking)이라고 한다.
- 이전 프레임의 포인트를 현재 프레임의 물체에 자동으로 누적하여 물체 해상도 및 보행자 분류 성능을 향상

### 4.1 단일 칼만 필터 기반

일반적으로 단일 객체 추적에 적용

Teichman의 연구[7]에선 단일 칼만 필터기반 추적기법을 이용하여 데이터를 누적시켜 분류의 성능을 높이고자 했다.

하지만 물체가 몇 개 없는 단조로운 시나리오에서 전후 프레임 간에 일치되는 물체관계를 이미 알고 있다고 가정하여, 특별한 데이터 연계 방법 없이 해당 물체 정보들을 단일 칼만 필터만 사용해추적 및 누적하여 포인트 수 증가를 유도하였다.

```
[7] A. Teichman, J. Levinson and S. Thrun, “Towards 3D Object Recognition via Classification of Arbitrary Object Tracks,” International Conference on Robotics and Automation, Shanghai, China, May 2011.
```

### 4.2 GM-PHD 필터

Data Associateion까지 고려한 다중 객체 추적에 적용

이전 프레임의 포인트를 현재 프레임의 물체에 자동으로 누적하여 물체 해상도 및 보행자 분류 성능을 향상

```
이연주, 서승우, "GM-PHD 필터를 이용한 보행자 탐지 성능 향상 방법", 서울대, 2015
```


---

## 자율 주행 차량의 다중 물체 추적 알고리즘
> 이재준, 한국기술교육대학교, 2015

군집화시키고 각각의 군집들 을 추적(Tracking)하면 물체의 크기, 속도 등과 같이 더 많은 정보를 추출하는 것이 가능하다


본 논문에서 소개하는 물체 추적 알고리즘의 구성
- 데이터 군집화(Data Clustering)
- 데이터 관계 분석(Data Association)
- 상태 추정(State Estimation)
- 데이터 정리(Data Arrangement)


### 2.1 데이터 군집화(Data Clustering)

우선 데이터를 시간 순서대로 나열하여 생성된 2D Depth Image 내에서 지역 탐색을 이용하여 빠르게 군집화[1]를 수행한다


False separations 을 제거하기 위하여 군집들을 병합하는 단계를 추가로 수행
- 병합과정은 전역 탐색으로 이루어진다

```
[1] J. B. Trevor, S. Gedikli, R. B. Rusu, H. I. Christensen ,“Efficient Organized Point Cloud Segmentation with Connected Components,”
```

### 2.2 데이터 관계 분석(Data Association)

데이터 관계 분석은 과거의 데이터를 통해 예측한 데이터와 새롭게 관측된 데이터의 관계를 분석하는 단계이다.

관계 분석 과정에는 2 가지 중요한요소가 있다.
- 특징(Feature)의 선택
- 일반적으로 위치 특징이 주로 특징 벡터로 사용되며 높이, 길이, 너비 등이 추가적인 특징으로 사용된다.
- 하지만 LIDAR 의 특성상 때때로 길이, 너비등과 같은 특징은 움직이는 물체들에서 심하게 변동하는 특성을 보이기 때문에 위치와 높이만을 사용하였다.
- 할당(Assignment) 전략
- 모든 군집과 추적 물체조합의 거리의 합을 근사적으로 최소화시키는 GNN(Global Nearest Neighbor)의 근사(Approximation)방식을 사용하였다.
- 할당 전략은 군집-추적물체 테이블에서 가장 낮은 거리의 조합부터 차례대로 할당해 나가는 전략[2]을 취하였다.

```
[2] F. Bourgeois and J. C. Lassalle, “An Extension of the Munkres Algorithm for the Assignment Problem to Rectangular Matrices.” Communications of the ACM, vol. 14, no. 12, p. 802, December, 1971.
```


### 2.3 상태 추정(State Estimation)

상태 추정 과정은 데이터 관계 분석을 통해 얻은 대응 관계를 이용하여 측정값(군집)으로 그에대응하는 추적 물체의 상태를 갱신하는 단계이다.

상태 추정은 **등속 선형 운동 모델**을 가정하여 수행되었고 상태 추정 알고리즘으로는 **칼만 필터**를 사용하였다[4].

상태 벡터는 위치와 속도만으로 구성된다.

### 2.4 데이터 정리(Data Arrangement)

데이터 정리 과정에서는 불필요한 데이터의 삭제와 새로운 데이터의 등록이 이루어진다.

데이터의 등록은 새로운 물체가 나타나는 즉시 실행되지만 삭제는 시간 지연을 두고 실행되어 잡음, 가려짐(occlusion)등에 의해 물체가 센서의 시야에서 사라지는 현상에 더 강인하게 동작할 수 있도록 하였다.

하지만 때때로 이런 지연전략이 추적 물체 목록을 비대하게 만들 수 있기 때문에 상대적으로 관측 횟수가 적은 물체에는 더 작은 시간 지연을 부여하여 불필요한 리소스 소모를 줄였다.

---

## [추천] [Object Tracking using OpenCV (C++/Python)](https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/)

Tracking 정의 : locating an object in successive frames of a video


### OpenCV 3.2에서 지원 하는 Tracker
- BOOSTING
- MIL
- KCF
- TLD
- MEDIANFLOW
- GOTURN



### Object Tracking관련 아이디어들

- Dense Optical flow: These algorithms help estimate the motion vector of every pixel in a video frame.

- Sparse optical flow: These algorithms, like the Kanade-Lucas-Tomashi (KLT) feature tracker, track the location of a few feature points in an image.

- Kalman Filtering: A very popular signal processing algorithm used to predict the location of a moving object based on prior motion information. One of the early applications of this algorithm was missile guidance! Also as mentioned here, “the on-board computer that guided the descent of the Apollo 11 lunar module to the moon had a Kalman filter”.

- Meanshift and Camshift: These are algorithms for locating the maxima of a density function. They are also used for tracking.

- Single object trackers: In this class of trackers, the first frame is marked using a rectangle to indicate the location of the object we want to track. The object is then tracked in subsequent frames using the tracking algorithm. In most real life applications, these trackers are used in conjunction with an object detector.

- Multiple object track finding algorithms: In cases when we have a fast object detector, it makes sense to detect multiple objects in each frame and then run a track finding algorithm that identifies which rectangle in one frame corresponds to a rectangle in the next frame.

### Tracking vs Detection


> 추가 내용 살펴 보기 : https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/

