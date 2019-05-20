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


```
[참고] Track-before-detect (TBD) : Tracking without a Detector 
- 탐지기 없이 센서 값을 바로 MOT에 적용 
    - eg. Radar-based tracking, low Signal-to-noise-Ratio 
- 추적 기법에 일반적이지 않음 --> 본 수업에서 다루지 않음 
```

![](https://i.imgur.com/RWZObEV.png)

#### 1.1.4 Different Types of Tracking

##### 가. Point Object Tracking 

- At most one detection per object, per time step 
    - eg. 이미지 탐지의 바운딩 박스, 비행기 탐지용 radar
    
##### 나. Extended Object Tracking 

- Possible more than one detection per object, per time step 
    - eg. Lidar로 한물체의 여러개의 포인트 접촉, 차량 탐지용 radar
    
- Possible to also estimate the extent (shape and size)

##### 다. Group Object Tracking 

- Several objects treated as single entity : A GROUP

- Possibly more than one detection per group, per time step 