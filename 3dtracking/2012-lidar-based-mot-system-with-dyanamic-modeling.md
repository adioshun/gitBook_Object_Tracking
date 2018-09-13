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





















