## 1. Introduction to Multi-object Tracking 

[![Alt text](https://img.youtube.com/vi/ay_QLAHcZLY/0.jpg)](https://www.youtube.com/watch?v=ay_QLAHcZLY)

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


#### 1.3.3 Measurement Modelling


센서의 종류와 탐지 대상에 따라 다르다. 

Describes relation between objects state and measurement 


[](https://i.imgur.com/HO7XITt.png)



![](https://i.imgur.com/91yOrqt.png)

So let's have a look at an example where we have Gaussian distributed measurement noise.

So the density for the measurement noise is Gaussian with 0 mean and covariance R.

If we have a measurement model with additive noise, then we get a Gaussian measurement likelihood.

So the density for the measurement z given the state x is Gaussian with mean described by the measurement function h with the object state as input, and the covariance is the measurement noise covariance, R.


#### 1.3.4 Sufficient Modelling

그럼 모델링은 어느 수준까지 해야 하나? 모델들은 100%완전할 필요는 없다 **sufficiently accurate**하고 **reasonable complexity**이면 된다. 
- high quality estimation 
- reasonable computation cost 

둘 사이의 적절한 밸런스만 유지 하면 된다. 


> 정확한 모델링을 위해 자동차의 바퀴 4개, 각 조향..등등을 다 안하고, 앞바퀴-뒷바퀴-조향 만 모델링 해도 된다. 



#### 1.3.5 Prediction, update, likelihood

![](https://i.imgur.com/20uIQ5w.png)


Given that we have a motion model and a measurement model, let's return to the Bayesian filtering recursion.
The first step in the recursion is known as the Chapman-Kolmogorov prediction.
Here we take the density at time k minus 1,given measurements up to and including time k minus 1,and we also take the transition density,and then we marginalize the previous state.

In other words, we marginalize the state at time k minus 1.
What this does is that it gives us the predicted state density, in other words, the density of the state at time k, given measurements up to and including time k minus 1.

The second step is the Bayes update.

Here we take the predicted density, the density of the state at time k, given measurements up to and including time k minus 1.

And we also take the measurement likelihood, so the density of the measurement z, given the state,
and then we normalize this.

And this gives us the updated density, the density of the object state x at time k, given measurements up to and including time k.

So we can see that the predicted density is used in the Bayes update.

And the updated density is then used in the next prediction.

And this gives us the Bayesian filtering recursion.

We predict the posterior density. 

We do a Bayes update and then we repeat this.

In multiple object tracking, the normalizing constant in the Bayes update is sometimes called the predicted likelihood.

What we have here is the predicted object density, given measurements up to time k minus 1, and the measurement likelihood.

And these two densities multiplied give us the joint density of the measurement and the object state.

And when we then marginalize the object state, we get just the density for the measurement.





![](https://i.imgur.com/71kMpm2.png)

We have a predicted likelihood that has been obtained by marginalizing some **predicted state density** and some **measurement likelihood**.

두개의 센서 측정을 가정하자. `Now let's assume that we have two different measurements, valued 2.5 and 6.9.`

추적기를 위해 아래가 2가지를 알아야 한다. `In a tracking context, `
- we have to reason about which of these two measurements should be associated to the state.
- We also have to reason about how probable each alternative association is.

**predicted likelihood**를 이용하여 알수 있다. `And we can do this using the predicted likelihood. `

In this case, we find that 
- the measurement equal to 2.5 has the predicted likelihood of about 0.3, whereas the measurement equal to 6.9 has the likelihood of much, much less.

In other words, the measurement value 2.5 is the most likely measurement of these two.

And if we had to make a decision which of these two measurements we should associate to the object, a good decision would be to take the most likely one.

Later in this course we're going to learn about how we can use the predicted likelihoods for multiple objects to reason about data association.




#### 1.3.6 Estimators and Performance Evaluation

아래 경우 posterior density를 이용하여 **object estimate**를 계산해야 하는 경우가 있다. `sometime it is necessary to compute an object estimate using the posterior density`
- MOT결과 시각화 
- 성능 평가 

![](https://i.imgur.com/88hkycy.png)




![](https://i.imgur.com/HUMMmHt.png)


---

#### 1.4.1 Kalman Filter Review

MOT에서는 모션모델과 측정모델이 비선형 경우가 많다 따라서 칼말필터 말고 다음 non-linear kalman를 사용한다. 
- Extended kalman filter
- Sigma-point kalman filter
    - unscented kalman filter(UKF)
    - cubature kalman filter(CKF)


MOT에서 highly non-linear 시나리오일경우에는 다음을 사용한다. 
- particle filter 

> 대부분의 MOT 경우 particle filter까지는 안써도 된다. 



---


#### 1.5.1 Assumed Density Filtering


http://luiarthur.github.io/ucsc_notes/advBayesComputing/14/





