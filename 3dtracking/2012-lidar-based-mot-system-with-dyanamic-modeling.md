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
- Filtering 



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

```
[5] Y. Bar-Shalom and T.E. Fortman, “Tracking and Data Association,” Academic Press, 1988
```

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
    
```
[28] C. C. Wang, C. Thorpe, and S. Thrun, “Online simultaneous localization and mapping with detection and tracking of moving objects: Theory and results from a ground vehicle in crowded urban areas,” IEEE International Conference on Robotics and Automation, Vol. 1, Sept. 2003, pp. 842–849
[35] T. D. Vu, O. Aycard, and N. Appenrodt, “Online localization and mapping with moving object tracking in dynamic outdoor environments,” IEEE Intelligent Vehicles Symposium, Istanbul, Turkey, June 2007
[66] R. A. Maclachlan, “Tracking of moving objects from a moving vehicle using a scanning laser rangefinder,” IEEE Intelligent Transportation Systems Conference, Toronto, Canada, Sept. 2006
```   
    
![](https://i.imgur.com/vSviMed.png)
동일 물체라도 angle문제로 Distance가 서로 다르다.     

해결책 #1: Adaptive Distance Threshold `A possible solution to this problem has been suggested by Sparbert et al. and Mendes et al. who used an adaptive distance threshold to perform segmentation [29, 30].`
- Their methods are based on the distance between data point to the LIDAR. 
- In their method any two consecutive points $$r_k$$ and $$r_{k+1}$$ will be regarded as belonging to the same object if the distance between them $$r_{k,k+1}$$ fulfill the Equation 2.1: (공식은 해당 논문 참고)
- 위 해결책은 노이즈 포인트에 잘 대처 하지 못함 `Because the algorithm mentioned above is based on the consecutive beams, it is very sensitive to the noise point.`

```
[29] J. Sparbert, K. Dietmayer, and D. Streller, “Lane detection and street type classification using laser range images,” IEEE Intelligent Transportation System Conference, Oakland, CA, USA, Aug. 2001
[30] A. Mendes, L. C. Bento, and U. Nunes, “Multi-target detection and tracking with a laser-scanner,” IEEE Intelligent Vehicles Symposium, Parma, Italy, June 2004
```

해결책 #2 : DBSCAN `Therefore, in this thesis, a density-based spatial clustering algorithm is applied for data segmentation. This clustering algorithm is a well-known data mining method named “Density-Based Spatial Clustering of Applications with Noise” (Figure 2.3) [31].`

> 자세한 DBSCAN의 설명 및 장점은 논문 참고 
> 본 논문에서 제안 하는 DBSCAN 파라미터 
> - The minimum number of points required to form a cluster is set to 2. 
> - The distance is empirically chosen as 120cm.

```
[31] M. Ester, H. Kriegel, J. Sander, X. Xu, “A density-based algorithm for discovering clusters in large spatial databases with noise,” proc. 2nd Int. Conf. on Knowledge Discovery and Data Mining, Portland, OR, USA, 1996, pp. 226
```

#### C. Occlusion

![](https://i.imgur.com/j5LgoWY.png)

정의 : the shadow of one object may partially block the view of a second object, causing segmentation to try to classify the single second object as several different objects moving in unison (Figure 2.4). 


해결책 #1 : a geometric vehicle model that requires continuity between disjoint point segments [47, 52, 81]. 

해결책 #2 : by performing image processing approaches before clustering step. 
    - the LIDAR image is processed as a 2D birds-eye-view image, 
    - and afterwards image-processing methods are applied.
    - eg #1. Zhao and Thorpe used **Hough transformation** to extract the lines [22]
    - eg #2. Burke applied a **median filter** following PCA [40].
    

```
[47] A. Petrovskaya and S. Thrun, “Model based vehicle tracking in urban environments,” IEEE International Conference on Robotics and Automation, Workshop on Safe Navigation, Vol. 1, 2009, pp. 1–8
[52] T. Ogawa, H. Sakai, Y. Suzuki, K. Takagi, K. Morikawa, “Pedestrian detection and tracking using in-vehicle lidar for automotive application,” IEEE Intelligent Vehicles Symposium, Baden-Baden, Germany, June 2011
[81] O. Aycard, “Contribution to perception for intelligent vehicles,” PhD thesis, Universite de Grenoble, France, 2010

```

#### D. Classification


방법 #1 : 물체별 속도로 구분 (사람 5mph, 자동차 5mph+)


방법 #2 : laser-based multi-object tracking system has been studied extensively [29, 30, 34, 36]

```
[29] J. Sparbert, K. Dietmayer, and D. Streller, “Lane detection and street type classification using laser range images,” IEEE Intelligent Transportation System Conference, Oakland, CA, USA, Aug. 2001
[30] A. Mendes, L. C. Bento, and U. Nunes, “Multi-target detection and tracking with a laser-scanner,” IEEE Intelligent Vehicles Symposium, Parma, Italy, June 2004
[34] C. Premebida and U. Nunes, “A multi-target tracking and GMM-classifier for intelligent vehicles,” IEEE Intelligent Transportation Systems Conference, Toronto, Canada, Sept. 2006
[36] F. Nashashibi and A. Bargeton, “Laser-based vehicles tracking and classification using occlusion reasoning and confidence estimation,” IEEE Intelligent Vehicles Symposium, Eindhoven, The Netherlands, June 2008
```


방법 #3 : Voting `Mendes, et al. uses a voting scheme presented by [37].`
- By considering all the hypotheses over time, an object is assigned with a class until the confidence level reaches a reasonable value [30]. 
- Although the features used are not discussed in detail, the results showed that voting classification approach can assign the right class after several frames (Figure 2.5).

```
[37] T. Deselaers, D. Keysers, R. Paredes, E. Vidal, and H. Ney, “Local representations for multi-object recognition,” DAGM 2003, Pattern Recognition, 25th DAGM Symp, pp. 305312, September 2003
```


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

```
[5] Y. Bar-Shalom and T.E. Fortman, “Tracking and Data Association,” Academic Press, 1988
[35] T. D. Vu, O. Aycard, and N. Appenrodt, “Online localization and mapping with moving object tracking in dynamic outdoor environments,” IEEE Intelligent Vehicles Symposium, Istanbul, Turkey, June 2007
[38] F. Fayad and V. Cherfaoui, “Tracking objects using a laser scanner in driving situation based on modeling target shape,” IEEE Intelligent Vehicle Symposium, Istanbul, Turkey, June 2007
[52] T. Ogawa, H. Sakai, Y. Suzuki, K. Takagi, K. Morikawa, “Pedestrian detection and tracking using in-vehicle lidar for automotive application,” IEEE Intelligent Vehicles Symposium, Baden-Baden, Germany, June 2011
```

향상된 알고리즘[53,54] : advanced well-known Bayesian approaches are 
- 1) multiple hypothesis tracking (MHT) algorithm 
- 2) joint probabilistic data association (JPDA)

```
[53] S. S. Blackman, “Multiple hypothesis tracking for multiple target tracking,” IEEE Aerospace and Electronic Systems Magazine, Vol. 19, No. 1, 2004, pp. 5–18
[54] Y. B. Shalom, T. Kirubarajan, and X. Lin, “ Probabilistic data association techniques for target tracking with applications to sonar, radar and EO sensors,” IEEE Aerospace and Electronic System Magazine, Vol. 20, No. 8, Aug. 2005, pp. 37–56
```

최근 알고리즘 : Recently, a batch of multi-object tracking systems have achieved notable success by applying Markov chain Monte Carlo data association (MCMCDA) [55, 56, 57].
- 기존 알고리즘 : Unlike other data-association methods that seek to maintain or test all possible data assignments, 
- MCMCDA uses Markov chain Monte Carlo sampling [58]. 
- 활용예 : Vu, et al,applied this data association for laser-based tracking systems and obtained positive results [59]

```
[55] S. Oh, S. Russell, and S. Sastry, “Markov chain monte carlo data association for general multiple-target tracking problems,” IEEE Conference on Decision and Control, Atlantis, Paradise Island, Bahamas, Dec. 2004
[56] T. Zhao, R. Nevatia, and B. Wu, “Segmentation and tracking of multiple humans in crowded environments,” IEEE Transactions on Pattern Analysis and Machine Intelligence, 2008
[57] S. Oh, S. Russell, and S. Sastry, “Markov chain monte carlo data association for multi-target tracking,” IEEE Transactions on Automatic Control, Vol. 54, No. 3, Mar. 2009
[58] R. Karlsson and F. Gustafsson, “Monte carlo data association for multiple target tracking,” Target Tracking: Algorithms and Applications, Vol. 1, Oct. 2001
[59] T. D. Vu and O. Aycard, “Laser-based detection and tracking moving objects using data-driven markov chain monte carlo,” IEEE International Conference on Robotics and Automation, Kobe, Japan, May 2009
```


#### A. Greedy Nearest Neighbor (GNN) Filter


#### B. Joint probabilistic data association (JPDA)


#### C. Multiple Hypothesis Tracking (MHT)


### 2.5 Approaches for occlusion(맞물림) handling

사람이 많은 곳에서 서로 가려짐이 발생할경우 추적이 어렵게 된다. 

The temporary occlusion of the objects may lead to mismatch when they return to view. 

To maintain estimates of the tracks during occlusion, it is critical to have an estimate of the motion model of the objects during occlusion [64].

```
[64] R. Rosales and S. Sclaroff, “Improved tracking of multiple humans with trajectory prediction and occlusion modeling,” IEEE CVPR Workshop on the Interpretation of Visual Motion,1998
```


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

background subtraction is very useful 
- to separate the foreground and background, and 
- to remove noise

an occupancy grid map [25] is employed to detect moving objects.

```
[25] A. Elfes, “Occupancy grids : a probabilistic framework for robot percpetion and navigation,” PhD thesis, Carnegie Mellon University, 1989
```

To form the occupancy map, 

1. the field of the LIDAR view is separated into 40cm×40cm grids, which is empirically selected. 

2. At any time frame, 
    - if a grid is occupied by the segments detected by sensor, its corresponding value will be increased by 1 and 
    - if no segment detected in this gird, the value will be decreased by 1. 

3. After a reasonable time interval, the grids representing stationary obstacles will have a relatively high value and any segments in these grids will be regarded as stationary objects. 

4. The stationary map is formed by all the grids with high enough value. 

> In the experiment without temporary static objects, the map tends to be stable after 80 to 100 frames.

```python 
# table after 80 to 100 frames.
mapUpdate(oldM ap, D)
addMap = same size to oldMap with all grids are 1

for each beam j with valid value in data set D
    the value of corresponding grid of addMap plus 1

for the value of each grid V_m of the addMap
    if V_m >= 1
        V_m = 1
        
newMap = oldMap + addMap
return newMap
```

### 4.2 Segmentation and classification

1. Once the noise is removed from the raw data,

2. LIDAR scan is separated into different segments and classified by the similar rule-based classification method applied by Nashashibi [36].

3. After classifying, every segment will be marked by feature points for the convenience of data association.

```
[36] F. Nashashibi and A. Bargeton, “Laser-based vehicles tracking and classification using occlusion reasoning and confidence estimation,” IEEE Intelligent Vehicles Symposium, Eindhoven, The Netherlands, June 2008
```


![](https://i.imgur.com/nZE9cMP.png)

#### A. Segmentation

DBSCAN사용 


#### B. Partially occluded object detection

본 논문에서는 [38, 36]연구를 참고 하여, the partial occlusion can be detected by the distance information and classified as follows :
- Occluded one endpoint;
- Occluded both endpoints;
- Occluded middle part;

```
[38] F. Fayad and V. Cherfaoui, “Tracking objects using a laser scanner in driving situation based on modeling target shape,” IEEE Intelligent Vehicle Symposium, Istanbul, Turkey, June 2007
[36] F. Nashashibi and A. Bargeton, “Laser-based vehicles tracking and classification using occlusion reasoning and confidence estimation,” IEEE Intelligent Vehicles Symposium, Eindhoven, The Netherlands, June 2008

```

```python
# The pseudo-code of the occlusion detection is:
occlusionDetec(S, D)
for each segment i in S
    for each beam j in the 5 neighbor beams outside the endpoints of i
        if the distance of j is less the distance of corresponding endpoint
            D(j) = 1
return D
```

#### C. Object classification and feature extraction

룰 기반 분류 `Similar to the method mentioned by Nashashibi [36], a rules-based classification is performed to distinguish pedestrian and vehicles:`
- Segments with width less than 80cm are pedestrian;
- Segments with width larger than 80cm are vehicle candidates and will be fitted to **line shape** or **L shape**;
- L-shaped segments with both sides less than 80cm and no occlusion detection are vehicle.


#### D. Line and “L-shape” classification

The corner point is found by searching the distance between the points and the line formed by the two endpoints. 

가장 멀리 있는 포인트가 코너 포인트가 됨`The farthest point will be regarded as the corner point.`

After that, the segment will be separated into two parts and the **weighted line fitting**  will be applied to each part. 

If the angle between the two lines is 
- less than 45 degree, this segment will be marked as **line**. 
- Otherwise, it will be marked as **L-shape**. 

When the number of the points of either part is less than 3, 
- the segment will be marked as **line** since the information of this part is too vague to determine a feature.

![](https://i.imgur.com/2sIXbRf.png)



```python 
LlDistinguish(i)
for each point n in segment i
    d(n) = distance between n to the line formed by two endpoints
mark the point with greatest d as potential corner point C
divided i into two sides A, B based on C
if sizeof (A) <= 3 or sizeof (B) <= 3
    mark i as a line
    return
else
    lineA = weightedlineFit(A)*
    lineB = weightedlineFit(B)*
    a = angle between lineA and lineB
    if a < 45
        mark i as a line
    else
        mark i as a L shape
(* this part is presented in following section)
```


#### E. Robust line fitting

#### F. Weighted line fitting

#### G. Corner fitting

#### H. Feature points calculation

The feature points are used to represent a vehicle depend on the shape and occlusion situation of the segment of points representing the vehicle.

##### 가. vehicle-classified object

For a vehicle-classified object, the object may be in the shape of a line, an “L”, or be uncertain. 

For a line segment, the two endpoints can serve as feature points. 

For this line representation, any occluded endpoints are deleted. 

For an “L-shaped” object, the corner point will also be included as a feature. 

If no feature point is detected, the mean point of the whole segment will be counted as the feature point. 


##### 나. For pedestrian-classified objects

For pedestrian-classified objects, the feature point is represented by the mean point of the segment.

Figure 4.13 illustrates some examples of the feature points calculation.

![](https://i.imgur.com/8sAxXyf.png)



### 4.3 Data association

Greedy Nearest Neighbor (GNN) 알고리즘 사용 
- the Mahalanobis distance is used to measure the distance instead of Euclidean
distance 
- because it(=Mahalanobis distance) takes into account the distribution of the data

![](https://i.imgur.com/qw7nNeg.png)

#### A. GNN data association


![](https://i.imgur.com/TA6CjPP.png)

Shown in Figure 4.15 are two consecutive frames of the same object (red circles).

검은 십자가는 4개의 모서리 특징점(Corner Feature points)이다. `The black crossings are the four corner feature points of the vehicle. `

Since the error or accuracy of the sensor, there is gap between two edges of the right angle. 

In the first frame (shown at left),
- the gap is notable such that the DBSCAN regarded them as different clusters and association
step marks the horizontal edge as an “adding” object (blue circles). 

In the new frame (shown at right), 
- the object is tracked successfully again because the older objects have priority to match
to the segments. 

The artificial “added” object is deleted since it does not last for enough time

#### B. Feature point association




### 4.4 Model motion

Similar to Lim used in visual tracking system [83], a general time series dynamic model is applied in this work to predict the state of targets during occlusion.

```
83] Hwasup Lim, “Dynamic motion and appearance modeling for robust visual tracking, ” PhD thesis, The Pennsylvania State University, 2007
```

#### A. Dynamic modeling for motion model


In this thesis, the motions considered include at least 
- constant velocity, 
- constant acceleration,
- geometric turning.



## 5. Experimental Results


## 6. Conclusion








