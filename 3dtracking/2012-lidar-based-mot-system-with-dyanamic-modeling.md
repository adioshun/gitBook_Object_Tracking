[LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf): 2012, 석사 학위 논문 





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

















