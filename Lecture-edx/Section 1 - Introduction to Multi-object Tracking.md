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

> 본 강좌에서는 이 경우에 대해서만 다룸 

##### 나. Extended Object Tracking 

- Possible more than one detection per object, per time step 
    - eg. Lidar로 한물체의 여러개의 포인트 접촉, 차량 탐지용 radar
    
- Possible to also estimate the extent (shape and size)

##### 다. Group Object Tracking 

- Several objects treated as single entity : A GROUP

- Possibly more than one detection per group, per time step 

- 그룹자체의 움직임에 관심 있을때 

![](https://i.imgur.com/830F0ei.png)


##### 라. Tracking with multi-path propagating 

![](https://i.imgur.com/aaArjUK.png)

- 탐지 에러등으로 한 물체에 대해 여러 탐지가 이루어 지는 경우 
    -eg. 바닦에 튕긴 전파가 차의 후면이 아닌 중간 바닦에 닿는 경우 

##### 마. Tracking with unresolved objects (=Tracking with merged Measurements)

- Multiple object cause a single detection 
    - eg. 붙어 있는 차량이 동일한 속도로 이동시 Radar는 하나로 인식 


---

#### 1.2.1 Challenges in MOT

![](https://i.imgur.com/6e1wRzE.png)

- 물체의 수 모름 
- 물체의 상태 모름 
- 물체가 움직임 
- 물체가 사라지고, 나타남
- 물체가 가려짐 
- 탐의 불안정 

#### 1.2.2 Imperfect Detections


- Missed detection : 탐지 실패 
- False Detection : 물체가 아닌데 탐지한 경우 

#### 1.2.3 Data Association Uncertainties

![](https://i.imgur.com/iaFDHy9.png)

![](https://i.imgur.com/0OZ11BJ.png)

---

#### 1.3.1 Bayesian Filtering Review

> MOT 는 Bayesian method를 해결 하는 문제이다. 

아래 기술들에 대하여 알고 있어야 한다. 
- Recursive estimation, Bayesian Statistics, bayes thorem
- Linear and non-linear filtering
    - Kalman filter
    - Non-linear Kalman filter
    - Particle filter
- Simple motion and measurement modeling 


베이지안 필터링은 Motion과 Measurement Modelling을 필요로 한다. 
- For Bayesian MOT, we need models for the multiple objects, 
    - how they move
    - how they enter/leave the surveillance area
    - how the detector works

- Such multiple object motion models, and multiple object measurement models, partly build upon models for single oblject:
    - single object **motion model**
    - single object **measurement model** 
    
- single object models integrated into multi-object models 



#### 1.3.2 Motion modelling


- 정의 : 물체가 어떻게 움직이는가를 모델링 한것. 즉, object state가 시간에 따라 발전하는가. `Describes how the tracked objects move; how the object state evolves over time'

- Data Association에도 중요한 역할을 한다.  


- Common models 
    - Linear : Constant velocity, Constant acceleration
    - Non-Linear : Coordinated turn 




![](https://i.imgur.com/tKPgJqn.png)

So let's consider an example where we have a constant velocity motion model.

We have the state at time k, and it consists of position and velocity.

In this case, a suitable motion function would be the following that you can see here on the screen.

The position at time k is given by the position at time k minus 1, plus the sampling time, t, multiplied by the velocity at time k minus 1.


And then we add some noise to this.

Since we have a constant velocity motion model, the velocity at time k is given simply by the velocity at the previous time step, k minus 1, plus some noise.


![](https://i.imgur.com/RcjZX0M.png)

So let's consider an example where we have Gaussian distributed process noise.
We assume it has a probability density function--that is, Gaussian with mean 0 and covariance Q.
With a motion model with additive noise, we get a Gaussian transition density.
So the density of the state at time k, given the state at time k minus 1, is a Gaussian PDF, with mean given by the motion function , f, with the previous state as input and a covariance, Q.



































