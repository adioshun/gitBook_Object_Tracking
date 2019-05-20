## 1. Introduction to Multi-object Tracking 

### 1.1 Introduction to Multi-object Tracking 

#### 1.1.1 Introductory Examples 

- 응용분야 소개 
- 역사 : 2차 세계 대전 
- 본 강의에서는 자율 주행용 추적 시스템에 초점 

#### 1.1.2 Multi-object Tracking Defintions

- Single object tracking is an example of a **filtering** problem.

- So what we are dealing with is the sequential processing
of noisy sensor measurements to determine the **object's state**.
    - object's position
    - properties that describe its motion
    - speed ,direction

- multiple object tracking 
    - determining the number of objects.
    - determining the object states.
    
> 물체의 수를 알고 있다면, the multiple object tracking problem is simplified.

#### 1.1.3 Tracking Based on Detections

![](https://i.imgur.com/hNNpUal.png)

- 추적은 탐지(measurements = detections )로 부터 시작 된다. 
- MOT알고리즘의 결과물은 **Posterior densities for objected states **
