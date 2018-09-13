[3D-LIDAR Multi Object Tracking for Autonomous Driving](https://www.slideshare.net/adioshun/3dlidar-multi-object-tracking-for-autonomous-driving-111277160): A.S. Abdul Rachman,석사 학위 논문, 140page


# Multi Object Tracking

![](https://i.imgur.com/cMfis3G.png)

> tracking-by-detection 모델(탐지와 추적이 연속적으로 이루어짐)


### 1. On the detection stage, 

segmentation of the raw data is done to build basic feature of the scanned objects and to distinguish between dynamic and static objects. 

Subsequently, the segmented objects pose is then estimated based on either its outlier feature or fitting the measurement into known model[28]. 

At this stage, the raw measurement has already been translated into refined measurement with meaningful attributes (e.g. the static/dynamic classification and the objects pose). 

In another word, the object is successfully detected. 


Subsequently, the detected object is given to state estimation filter so that object kinematic states can be predicted according to a dynamic motion model. 

The purpose of the tracker is to effectively estimate the possible evolution of the detected object states even in the presence of measurement uncertainties, an optimal Bayesian filter such as Kalman Filter and Particle Filter are extensively used to address state uncertainties due to unmodelled dynamics of target evolution or noise acting on measurement.



## 2. data association (DA)

Next, a data association (DA) procedure is done by assigning detected object into a track with established filter state or newly started trajectory. 

The purpose of DA is to ensure the detected objects are localized while simultaneously maintaining their unique identity. 

At this stage uncertainties of the measurement due to finite sensor resolution and/or detection step imperfection may arise 

In order to address this issue, Bayesian probabilistic approaches are commonly used to handle DA process
- Joint Probabilistic Data Association Filter (JPDAF)[29] 
- Multiple Hypothesis Tracking (MHT)[30].


## 3. 

Finally, in practice a track management is required to cancel out spurious track based on specific criteria. 

Track management is responsible for handling existence and classification uncertainties based on a sensor-specific heuristic threshold. 

For example, track existence is defined to be true if 90% of its trajectory of track hypothesis is associated with a highly correlated measurement. 

The same also applies with class uncertainties; object class can be determined based thresholding of dimension, past motion, or visual cue (i.e. colour). 

Alternatively, these two uncertainties can also be assumed to be a random variable evolving according to Markovian
process. 

The Integrated Probabilistic Data Association[31] specifically model the existence of track as binary Markov process.

## 추가 팁 

In a typical urban scenario, sensor occlusions are unavoidable occurrences, to address this several works try to explicitly model occlusion[32, 33, 34] during detection and incorporated occlusion handling in their object tracking method. 

In the inter-process level, one notable approach as proposed by Himmelsbach[25] is the bottom-up/top-down approach which lets the tracker and detector exchange stored geometrical information to refine the detection parameter.

Alternatively, some other works have proposed a track-before-detect method that avoids explicit detection that takes sensor raw data as an input for tracking process[35].

> 여러 Lidar를 이용한 front-back/back-front 기법은 어떤가? 


## 3. Tracking Fundamentals

### 3.1 Overview

![](https://i.imgur.com/EW4cpdY.png)

1. The result of detection is used to start a new track, or if existing track exists, the measurement is checked
if it statistically likely to be correct measurement through gating. 

2. Passing the gating is the prerequisite of association between measurement and tracks before being sent forward to state
estimator. 

This chapter shall cover the assumed modelling of sensor and target dynamics, used not only in state estimatio and prediction, but also Data Association. 

Accordingly, several classes of Bayesian filter will be introduced.


### 3.2 Sensor and Target Modelling

The LIDAR sensor is placed on moving ego-car, which is considered as the origin. 

Due to the measuring principle of rotating LIDAR sensor the measurement originally comes in polar coordinates (in the form of distance and bearing). 

However, Velodyne digital processing unit readily provides the sensor measurement on the Cartesian coordinate system, 

In this thesis, the latter coordinate system will be used to conform better with ego-vehicle navigation frame. 

The relation between the ego-car navigation frame and sensor measurement frame can be seen in Figure 3-2.


> ???

### 3.3 Object Tracking as A Filtering Problem

In this thesis, object tracking problem is modelled as a filtering problem in which the object states are to be estimated from noisy, corrupted or otherwise false measurements. 

The estimated states and assumed system dynamics are given in the previous section. 

The basic concept of Bayes filtering is introduced along with the filters which will be used during implementation.


#### A. Bayes Theorem in Object Tracking


#### B. Unscented Kalman Filter

#### C. Interacting Multiple Mode


#### D. Data Association Filter

칼만필터가 예측값의 최적화를 지원 하긴 하지만 `KF (or its variant) offers the ability to provide optimal estimates of an object track. `

그럼에도불구하고  센싱의 불확실성으로 인해서 추적 물체가 해당 물체가 맞는지 보장 할수 없다. `Notwithstanding, due to measurement uncertainty there is no guarantee that the tracked object is actually a relevant object, or even if it is an existing object in the first place. `

따라서 후속적인 분류및 확인 절차가 필요 하다. `Therefore, a subsequent classification and validation of the estimated track are simply necessary.`

Data Association (DA) is a process of associating the detection result into a tracking filter.

There are two classes of DA filter: 
- the deterministic filter and 
- the probabilistic filter. 


##### 가. NNF

- Representative of deterministic DA filter is Nearest Neighborhood Filter (NNF) algorithm 

- NNF updates each object with the closest measurement relative to the state. 

- NNF associates object with known track based on the shortest Euclidean or the Mahalanobis distance between the
measurement and track.

##### 나. PDAF

- The probabilistic DA filter that is very well-known in object tracking literature body is the
eponymous Probabilistic Data Association Filter (PDAF)[29]. 

- The PDAF perform a weighted update of the object state using all association hypotheses in order to avoid hard, possibly erroneous association decisions commonly encountered in the use of NNF algorithm. 

- The erroneous association is often found during the scenario in which multiple measurements is located close to each other (i.e. clutter) and results in single measurement being used to incorrectly update all other nearby objects.


> PDA is also one of the most computationally efficient tracking algorithms among clutter-aware tracker[97], for
instance when compared to MHT[117]. 


![](https://i.imgur.com/eJBHCLO.png)



### 3.4 Probabilistic Data Association Filter (단일)


### 3.5 JPDA: Tracking Multiple Target in Clutter (멀티)









