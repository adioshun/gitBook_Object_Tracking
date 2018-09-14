[LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf): 2012, 석사 학위 논문 

DBSCAN
DA : Greedy Nearest Neighbor (GNN)


## 1. Introduction

### 1.2 Multi-object tracking system

![](https://i.imgur.com/mBkE6k4.png)

#### A. detection

During the detection step, 
- the raw data obtained by the sensor is captured by the system, 
- and the foreground data is partitioned from background data and separated into differ-
ent segments. 

Once the foreground objects are detected and grouped, the problem of multi-object
tracking becomes the problem of estimating the dynamic states of each object. 

Generally, this estimation consists of two parts: 
- Data Association and 
- Filtering [5].

### B. Data Association

Data association seeks to match the observations from the sensor to corresponding existing tracked objects. 

### C. Data Filtering 

Filtering is applied to improve the estimate of the state by combining recent observations with **models of object behavior**.

This model is not only used for data filtering, but also for predicting the motion of any temporarily occluded targets.

## 2. Related Work


### 2.1 Historical development of laser-based tracking system

the problem of detecting and tracking multi-object generally consists of three parts:
- Detection
- Filtering
- Data Association [5]. 

Detection addresses the problem of extracting the foreground from the raw data. 

Filtering is applied to improve the estimate of the target state by combining the existing model and observation. 

Data association deals with matching the observations from the sensor to existing tracked objects. 
- This “matching” process for moving objects can be extremely hard for crowded scenes.


### 2.2 Moving objects detection for laser-based tracking system

#### A. Background subtraction

Most tracking systems apply a “background filter” first before processing the data
- Goal of a background filter : separate the foreground and background, and to remove noise

Background subtraction techniques have been widely used for detecting moving objects from static cameras [23]. 

```
[23] M. Piccardi, “Background subtraction techniques: A review,” IEEE International Conference on Systems, Man and Cybernetics, 2004, pp. 3099–3104
```

One approach, presented by Fod et,al., considers the different features provided by LIDAR within a background model based on range information [24]. 

```
[24] A. Fod, A. Howard, and M. J. Mataric, “Laser-based people tracking,” IEEE International Conference on Robotics and Automation, Washington DC, May, 2002, pp. 3024–3029
```

In order to simultaneously detect moving targets and maintain the position of stationary objects, an occupancy grid map is employed to detect moving objects [25]. 

```
[24] A. Fod, A. Howard, and M. J. Mataric, “Laser-based people tracking,” IEEE International Conference on Robotics and Automation, Washington DC, May, 2002, pp. 3024–3029
```

The grid-based map technique has been widely used in Simultaneous Localization and Mapping (SLAM) for representing complex outdoor environments (Figure 2.1) [7, 35, 59]. 


```
[7] C. C. Wang, “Simultaneous localization, mapping and moving object tracking,” PhD thesis, The Robotics Institute, Carnegie Mellon University, Pittsburgh, PA, Apr. 2004
[35] T. D. Vu, O. Aycard, and N. Appenrodt, “Online localization and mapping with moving object tracking in dynamic outdoor environments,” IEEE Intelligent Vehicles Symposium, Istanbul, Turkey, June 2007
[59] T. D. Vu and O. Aycard, “Laser-based detection and tracking moving objects using data-driven markov chain monte carlo,” IEEE International Conference on Robotics and Automation, Kobe, Japan, May 2009

```


Due to the few features extracted from LIDAR data, by building motion-map and stationary-map separately, Wang showed this approach is more robust than a feature-based approach (Figure 2.1) [7].


#### B. Segmentation

The data segmentation process seeks to 
- divide the collected data points into distinct segments 
- such that points associated with the same object are grouped together. 


거리 기반 방식으로 세그멘테이션 `As a first criterion, a common method is to perform segmentation based on a distance threshold. `
    - Examples : Wang et al., Maclanchlan and Mertz and Vu et al. [28, 35, 66].

한 물체의 연속적인 점들 도출 `As the next step, consecutive(연속적) points on the same object are sought(구하다).`
    - 문제점 : This is challenging because of the limited angular resolution of the LIDAR sensor in this study. 
    - 빈번한 position/angle 변경시 더 큰 문제 `Specifically, the distance between two consecutive scan points on the same surface can change dramatically depending on the varying position and angle of the surface relative to the sensor. `
    
![](https://i.imgur.com/vSviMed.png)
동일 물체라도 angle문제로 Distance가 서로 다르다.     

해결책 #1: Adaptive Distance Threshold `A possible solution to this problem has been suggested by Sparbert et al. and Mendes et al. who used an adaptive distance threshold to perform segmentation [29, 30].`
- Their methods are based on the distance between data point to the LIDAR. 
- In their method any two consecutive points $$r_k$$ and $$r_{k+1}$$ will be regarded as belonging to the same object if the distance between them $$r_{k,k+1}$$ fulfill the Equation 2.1: (공식은 해당 논문 참고)
- 위 해결책은 노이즈 포인트에 잘 대처 하지 못함 `Because the algorithm mentioned above is based on the consecutive beams, it is very sensitive to the noise point.`

해결책 #2 : DBSCAN `Therefore, in this thesis, a density-based spatial clustering algorithm is applied for data segmentation. This clustering algorithm is a well-known data mining method named “Density-Based Spatial Clustering of Applications with Noise” (Figure 2.3) [31].`

> 자세한 DBSCAN의 설명 및 장점은 논문 참고 
> 본 논문에서 제안 하는 DBSCAN 파라미터 
> - The minimum number of points required to form a cluster is set to 2. 
> - The distance is empirically chosen as 120cm.

#### C. Occlusion

![](https://i.imgur.com/j5LgoWY.png)

정의 : the shadow of one object may partially block the view of a second object, causing segmentation to try to classify the single second object as several different objects moving in unison (Figure 2.4). 


해결책 #1 : a geometric vehicle model that requires continuity between disjoint point segments [47, 52, 81]. 

해결책 #2 : by performing image processing approaches before clustering step. 
    - the LIDAR image is processed as a 2D birds-eye-view image, 
    - and afterwards image-processing methods are applied.
    - eg #1. Zhao and Thorpe used **Hough transformation** to extract the lines [22]
    - eg #2. Burke applied a **median filter** following PCA [40].
    


#### D. Classification


방법 #1 : 물체별 속도로 구분 (사람 5mph, 자동차 5mph+)


방법 #2 : laser-based multi-object tracking system has been studied extensively [29, 30, 34, 36]

방법 #3 : Voting `Mendes, et al. uses a voting scheme presented by [37].`
- By considering all the hypotheses over time, an object is assigned with a class until the confidence level reaches a reasonable value [30]. 
- Although the features used are not discussed in detail, the results showed that voting classification approach can assign the right class after several frames (Figure 2.5).


### 2.3 Filtering methods for laser-based tracking system

목적 : Filtering is necessary to smooth the trajectory and to predict the vehicles pose state when the observation cannot be obtained directly. 

방법 `To perform this filtering,`
- Bayesian based filters : the Kalman Filter, the Extended Kalman Filter, the particle filter 
- The IMM algorithm


#### A. Kalman Filter

#### B. Particle Filter

### 2.4 Data association approaches for laser-based tracking system

목적:  Data association seeks to match data points to a specific object

Lidar기반 DA의 문제점 : Because of the limited features provided by the distance sensor,
accurate data association is very difficult, especially for crowded scenes.

가장 일반적 알고리즘 : Greedy Nearest Neighbor (GNN) filter [5]
- As the most intuitive approach to assign the nearest segment to the object
- 간담함, 직관적, 부하 적음, Reasonable ERROR , 많은 연구에서 활용 [35, 38, 52]

향상된 알고리즘[53,54] : advanced well-known Bayesian approaches are 
- 1) multiple hypothesis tracking (MHT) algorithm 
- 2) joint probabilistic data association (JPDA)

최근 알고리즘 : Recently, a batch of multi-object tracking systems have achieved notable success by applying Markov chain Monte Carlo data association (MCMCDA) [55, 56, 57].
- 기존 알고리즘 : Unlike other data-association methods that seek to maintain or test all possible data assignments, 
- MCMCDA uses Markov chain Monte Carlo sampling [58]. 
- 활용예 : Vu, et al,applied this data association for laser-based tracking systems and obtained positive results [59]


#### A. Greedy Nearest Neighbor (GNN) Filter


#### B. Joint probabilistic data association (JPDA)


#### C. Multiple Hypothesis Tracking (MHT)


### 2.5 Approaches for occlusion(맞물림) handling

사람이 많은 곳에서 서로 가려짐이 발생할경우 추적이 어렵게 된다. 

The temporary occlusion of the objects may lead to mismatch when they return to view. 

To maintain estimates of the tracks during occlusion, it is critical to have an estimate of the motion model of the objects during occlusion [64].


해결 방법 : 이전장에 언급한 filltering알고리즘에 기능을 추가 하여 해결 가능 `To some extent, this occlusion problem can be resolved using some of the previously-mentioned filtering methods necessary in laser-based tracking systems.`
- 움직임 예측 가능 : 칼만 필터 
- 움직임 예측이 불가능 함(칼만필터기반) : IMM(Interactive Multiple Model), 일반적으로 사용됨 
    - runs several Kalman Filters with different models parallel and merge the outputs to predict the positions [22, 28, 42, 52].
- 움직임 예측이 불가능 함(확률 기반) : 파티클 필터 
    - probability based model in a particle filter can deal with complex dynamic motion


#### A.Explicit model with Kalman Filter

#### B. Probability model with particle filter

#### C. Interacting Multiple Models (IMM)

#### D. Dynamic Model


## 3. System Setup

> 장비 구성 및 테스트 환경 

## 4. Methodology

![](https://i.imgur.com/B6ndvLa.png)

1. Each frame of the LIDAR data is pre-processed to remove noise and to extract foreground information from background information. 

2. Next, the data is separated into different segments and each segment is classified and labeled as either belonging to a vehicle or a pedestrian. 

3. During the data association step, the system tries to match an object to the
nearest segment with the same label
    - If a new segment cannot be associated to a previously-existing object, it is stored for a short period. Such stored segments are marked as missing and deleted if no prior or subsequent matches are found for several frames.
    - If a segment is not found to match a new object, and the object persists for a specific time interval, it is marked as a new object and added to the object list for future tracking.

4. Once the association is completed, each object’s position is predicted and correlated with incoming data using Kalman filters.

4. Objects remaining within a small boundary for a long time interval are marked as stationary.

5. If any object is marked as missing during the association step, its new position will be estimated by the dynamic model. 

6. Finally, the system obtains a new data frame and repeats the processing loop again.


### 4.1 Pre-processing





