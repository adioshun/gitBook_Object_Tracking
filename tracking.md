# Tracking

## 1. 정의 

### 정의 #1
Tracking 정의 : locating an object in successive frames of a video

![](https://i.imgur.com/zGOq9n2.png)

출처 : [Udacity](https://classroom.udacity.com/courses/ud810/lessons/3271928538/concepts/32865685380923)
- [Prediction](https://youtu.be/KsbjLtR_N0Y) 다시 살펴 보기 
- [Correction](https://youtu.be/KV7BKqrzeC4) 다시 살펴 보기 
- [Sumary](https://classroom.udacity.com/courses/ud810/lessons/3271928538/concepts/32865685430923) 다시 살펴 보기 

|![](https://i.imgur.com/r1AONhf.png)|![](https://i.imgur.com/biR0MMZ.png)|
|-|-|
|Filtering|Tracking|


### [정의 #2](http://srl.informatik.uni-freiburg.de/teachingdir/ws13/slides/11-TemporalReasoning-3.pdf)

- Detection is knowing the presence of an object, possibly with some attribute information

- Tracking is estimating the state of a moving object over time based on remote measurements

- Tracking also involves maintaining the identity of an object over time despite detection errors (FN, FP) and the presence of other objects

- Tracking may involve estimating the state of several objects at a time. This gives rise to origin uncertainty, that is, uncertainty about which object generated which observation

- Data association addresses the origin uncertainty problem. It’s the process of associating uncertain measurements to known tracks

- Data association may involve interpreting measurements as new tracks, false alarms or misdetections and tracks as occluded or terminated


---

## 2. 분류 

### [분류 #1](http://srl.informatik.uni-freiburg.de/teachingdir/ws13/slides/11-TemporalReasoning-3.pdf)

- Single non-maneuvering target, no origin uncertainty
  - Kalman filter (KF) or extended Kalman filter (EKF)

- Single maneuvering target, no origin uncertainty
  - KF/EKF with variable process noise
  - Multiple model approaches (MM)

- Single non-maneuvering target, origin uncertainty
  - KF/EKF with nearest/strongest neighbor data association
  - Probabilistic data association filter (PDAF)
  
- Single maneuvering target, origin uncertainty
  - Multiple model-PDAF (MM-PDAF)

- Multiple non-maneuvering targets
  - Joint probabilistic data association filter (JPDAF)
  - Multiple hypothesis tracker (MHT)
  - Markov chain Monte Carlo data association (MCMCDA)
  
- Multiple maneuvering targets
  - MM-variants of MHT (e.g. IMMMHT)
  - MM-variants of other data association techniques

### 분류 #8 

- 확률 기반: probabilistic data association [5], joint probabilistic data association [6], multiple hypothesis tracking [7] 
- 최적화 기반: Hungarian algorithm [16]
- 전역최적화 기반의 greedy 방법[17]

### 분류 #8 

- m-out-of-n기법 : n번 스캔에서 m번 연관된 정도를 살핌, 5회 미만 assign 실패시 Dead로 판단
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)


- 확률 기반 기법 : 연관필터에서 제공하는 존재 확률 기법 활용
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) 기법


- Assignment Problem = build a table of match scores

### 분류 #8 

#### Single Target Data Association

Non-Bayesian
- Nearest neighbor (NN)
    - Simple to implement
    - Can integrate wrong measurements (false alarms), and thus, produce overconfident estimates
    - Good if prediction and measurement models are accurate 

Bayesian
- Probabilistic Data Association Filter (PDAF)
    - A bit more involved to implement
    - Provide conservative estimates
    - Good in presence of high clutter and noisy models 
    

#### Multi-Target Data Association 

Non Bayesian approaches
- Nearest neighbor
- Interpretation tree
- Joint compatibility (JCBB)

Bayesian approaches
- JPDAF
- MHT
- MCMC 


```
- Bayesian: compute a full (or approx.) distribution in DA space from priors, posterior beliefs, and observations

- Non-Bayesian: compute a maximum likelihood estimate from the possible set of DA solutions 

- Nearest neighbours
    - choose the measurement with highest probability given predicted state
    - popular, but can lead to catastrophe
    
- Probabilistic Data Association
    - combine measurements, weighting by probability given predicted state
    - gate using predicted state



```
> [ref](http://luthuli.cs.uiuc.edu/~daf/tutorials/activity/Trackingbasicsblock.pdf)










### [분류 #2](https://github.com/nathanlem1/MTF-Lib)

- Traditional multi-target filters such as 
  - Global Nearest Neighbour (GNN), 
  - Joint Probabilistic Data Association Filter (JPDAF), 
  - Multiple Hypothesis Tracking (MHT), 
  - etc. 
  
- Random Finite Set (RFS)-based multi-target filtering algorithms such as 
  - Probability Hypothesis Density (PHD) filter, 
  - Cardinalized Probability Hypothesis Density (CPHD) filter, 
  - Cardinality Balanced Multi-Bernoulli (CB-MB) filter, 
  - Labeled Multi-Bernoulli (LMB) filter, 
  - Generalized Labeled Multi-Bernoulli (GLMB) filter, 
  - etc. 
  
- Stochastic populations-based filter such as 
  - Hypothesized and Independent Stochastic Population (HISP) filter, 
  - etc.


- Multiple target, multiple type filtering algorithm such as 
  - N-type PHD filter, 
  - etc


### 분류 #3 : 이미지 기반 트래킹

* 결정론적 방법 : Local Search
  * Least-Square tracking
  * Mean-Shift
  * Gradient ascent/decent 알고리즘
* 확률론적 방법 : Probabilistic search
  * Kalman Filter
  * extended kalman Filter
  * Particle Filter

### 분류 #4

Basic Tracking Algorithm

* centroid tracking : it relies on the Euclidean distance between
  * \(1\) existing object centroids \(i.e., objects the centroid tracker has already seen before\) and
  * \(2\) new object centroids between subsequent frames in a video.

Advanced Tracking Algorithm

* kernel-based
* correlation-based


### 분류 #5 

**이동물체 추적기법**은 그 처리방법에 따라 분류할 경우 **정합기반기법**과 **에너지기법**으로 분류할 수 있다.

정합기반기법

* 추적대상의 윤곽선, 모서리, 휘도 혹은 색상분포를 가지고 추적대상의 모델ㅇ르 구성하여 화면 내에서 이와 유사한 부분을 탐색하는 방법으로 탐색과 정합 두 가지 단계로 구성된다.
* 정합기반 방법은 탐색과정을 거쳐 이동물체의 이동 가능한 위치를 예측하며, 정합과정을 거쳐 이동물체의 이동 가능한 위치를 예측하며, 정합과정을 거쳐 예측위치에 대한 이동물체의 동일성 판별을 수행하게 된다.
* 정합기반 이동물체 추적기법은 전체적인 휘도 변화에 대한 적응능력이 좋으며, 배경과 위치의 변화가 발생할 경우에도 적용할 수 있다는 장점을 가지고있다.
* 그러한 추적대상의 프레임간의 변화가 클 경우 정합성능이 저하되고, 추적대상의 움직임이 고속인 경우 추적대상이 저주파 성분으로 이루어지기 때문에 정합을 위한 템플릿 추출에 어려움이 발생하게 된다.

에너지기반 이동물체 추적

* 광류, 능동외곽선, 레벨 셋 등과 같은 세부적인 분류가 있으며, 공통적으로 화소, 영역, 윤곽선 등과 같은 영상의 특징점이 프레임 간에서 에너지보존 법칙을 준수한다는가정을 기초로 한다.
* 즉, 짧은 시간 내에서 얻어지는 연속하는 두 프레임에 대하여 한 화소 또는 한 영역은 공간적인 변화만 존재하며, 밝기 값이나 분포, 즉 화소자체가 소유하고 있는 빛 에너지를 보존된다는 것이다.
* 이 기법은 계산량이 증가하지만 화면의 미세한 움직임까지 포착할 수 있으며, 추적 대상의 형태변화가 클 경우에도 강인간 추적 성능을 보여주는 장점을 가지고 있다.

### [분류 #6](http://docplayer.net/16497156-Moving-object-tracking-of-vehicle-detection-a-concise-review.html): 2015



* Tracking Methods
* Region-based tracking methods
* contour tracking methods
* 3D Model based tracking methods
* Feature based tracking methods
* Color and Pattern based tracking methods


> [상세](https://legacy.gitbook.com/book/adioshun/paper_2d-object-detection-and-tracking/edit#/edit/master/Tracking/2015-moving-object-tracking-of-vehicle-detection-a-concise-review.md?_k=1o66tn)

### [분류 # 7](https://pdfs.semanticscholar.org/25a6/c5dff9a7019475daa81cd5a7f1f2dcdb5cf1.pdf): 2014

![](https://t1.daumcdn.net/cfile/tistory/2469F54157F8B84417)

- point tracker : 매 프레임에서 탐지 수행 
- kernel, contour : object가 처음에 나타날 때만 detection 과정이 필요  

`For illustration, the point trackers involve detection in every frame; while
geometric area or kernel based tracking or contours-based tracking require detection only when the object first appears
in the scene. `



> [정리:A Survey on Object Detection and Tracking Methods](https://legacy.gitbook.com/book/adioshun/paper_2d-object-detection-and-tracking/edit#/edit/master/Tracking/2014-a-survey-on-object-detection-and-tracking-methods.md?_k=0wej7f)












---

## 3 . [Issues](https://www.youtube.com/watch?v=xChHuaPsq90)

- Initialization  
  - Manual 
  - 배경 제거 
  - Detection 
- Obtaining observation and dynamics model 
- Prediction vs. correction 
- Data Association 
- Drift : Errors caused by dynamical model, observation model, and data association tend to accumulate over time 

---





### Tracking vs Detection

> 추가 내용 살펴 보기 : [https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/](https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/)





# 각 알고리즘 설명 
그 중 Mean Shift, CAMshift ABCshift 알고리즘은 탐색 윈도우 를 통하여 추적물체의 영역 및 중심을 계산한다.

## Mean Shift\(평균이동알고리즘\)는

* 데이터 집합의 밀도분포를 기반으로 관심영역 객체를 고속으로 추적하는 알고리즘으로서 초기의 검색 영역의 크기와 위치를 지정하면 반복적인 색 분할 계산으로 색상 클러스터가 발생하고 초기 지정한 색 영역에 기반을 두어경계를 결정하여 관심 물체를 추출하게 된다\[4\].
* Tracks objects by finding the maximum density of a discrete sample of a probability function


## CAMshift
Mean Shift 알고리즘을 개량한 CAMshift 알고리즘은 1998년 GR Gradski에 의해 처음 소개되었다\[5\].

* Color Segment 방법의 Mean Shift 알고리즘을 연속적인 입력 영상에서 사용하기 위해 개선한 것으로 탐색 윈도우의 크기를 스스로 조정하는 기법을 사용하여 능동적으로 변화하는 객체의 크기를 검출하고 추적해낼 수 있다.

## ABCshift 알고리즘은

* CAMshift 방법과 유사하나 복잡한 색상의 배경에 적응하여 객체를 배경과 따로 분리하는 효과를 얻어서 객체와 같은 색상이 등장하는 상황 중에도 강인한 추적을 보인다\[7\]. 　

## 칼만 필터
칼만 필터, 확장 칼만 필터, 입자 필터는 오차가 포함된 현재 시스템 측정값이나 관측값을 바탕으로 미래정보를 예측하는 알고리즘이다.

칼만 필터는 루프만 칼만에 의해 1960년대 초 개발된 필터로 순환적선형구조로 되어 있고 단순하며 수렴 성이 좋다.

칼만 필터는 수식을 이용하여 직접적인 예측이 가능하므로 컴퓨터 시스템을 이용하여 추적할 때 적합한 방법이다\[8\].

그리고 입자 필터\(Particle Filter\)를 이용한 추적은 시스템에 가우시안 확률분포로 임의로 생성된 입력을 종합하여 추적이 이루어지도록 하는 방법이다.

* Particle Filter 알고리즘은 객체가 가려지는 상황에 강인하므로, 이 특성을 이용한 부분색상정보 기반의 추적 시스템이 개발되었다\[9\].
* 일반적으로 물체의 선형적인 운동에는 칼만 필터가 사용되고 비선형적 운동에는 확장 칼만 필터나 입자 필터가 사용된다.

Manya Afonso는 대표적인 비선형 예측 알고리즘인 확장 칼만 필터와 입자 필터에 대해 비교 분석하였다\[10\].

## 혼합방식 

위에 소개된 알고리즘들이 갖고 있는 장점을 취하고 단점을 보완하기 위해 각각의 알고리즘을 통합하여 객체를 추적하려는 시도도 이루어지고 있다.

그예로 칼만 필터와 CAMshift 알고리즘을 결합하여 추적객체의 가려짐에 강건한 추적에 관한 연구가 진행되었다\[11,12\].

* 탐색 윈도우 예측 시 물체의 속도만을 반영하고 CAMshift에 의해 구한 중심벡터 이동정보를 활용하지는 않았다.

색상객체의 추적을 위한 또 다른 추적모듈 결합방법으로 칼만 필터와 입자 필터의 결합에 대해 다룬논문도 소개되었다\[13\].

* 선형 필터인 칼만 필터는 선형 운동을 하는 객체의 추적을, 비선형 운동을 하는 객체의 추적은 입자 필터를 이용하여 추적한 점이특징이다.

또한, 추적되는 색상객체를 SURF 알고리즘을 이용하여 인식하고 칼만 필터를 결합하여 움직임을 예측한 방법도 연구된 바가 있다\[14\].

> CAMshift 기법과 칼만 필터를 결합한 객체 추적 시스템, 김대영, 2013


---




### 4.1 단일 칼만 필터 기반





---



