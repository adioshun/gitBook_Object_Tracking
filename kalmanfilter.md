# 칼만필터  [[홈페이지]](http://www.cs.unc.edu/~welch/kalman/)

* Fusion: Used to estimate a state of the system by combining **measurements** from different sources
* Prediction : Used to estimate a system **state**\(=velo, position\), where it cannot measure it directly, but an** indirect measurement** is available

> 참고 : 도대체 칼만필터란 무엇인가? [\[1\]](https://blog.naver.com/pjy6075/221228342912), [\[2\]](https://blog.naver.com/pjy6075/221244351376), [\[공식설명\]](https://blog.naver.com/dusrb2003/220272227990),[코드분석](http://msnayana.blog.me/80107534127), [책정리](http://msnayana.blog.me/80144116755), [영문매거진](http://academic.csuohio.edu/simond/courses/eec644/kalman.pdf)  
> 참고\(영문\) : [Object tracking with LIDAR, Radar, sensor fusion and Extended Kalman Filter](http://www.coldvision.io/2017/04/15/object-tracking-with-lidar-radar-sensor-fusion-and-extended-kalman-filter/), [Sensor Fusion Algorithms For Autonomous Driving: Part 1 ](https://medium.com/@wilburdes/sensor-fusion-algorithms-for-autonomous-driving-part-1-the-kalman-filter-and-extended-kalman-a4eab8a833dd)


## 용어 정리

- Prediction step
  - 입력 : 불확실한 값
  - 작업 : estimates with model
  - 출력 : state (=Estimation)

- Update Step
  - 입력 : Measurement
  - 작업 : Kalman filter correcting = Update(state of Measurement + predicted state)
  - 출력 :

- Estimation(=state) : 불확신한 Value(=Measurement)에 Model 정보를 이용하여 예측한값

- Measurement : 센서등을 통해 입력되는 값, 불확실성을 가지고 있음

```Python

#correct the Kalman with the current measurement, calculate the Kalman prediction,
current_measurement = np.array([[np.float32(x)],[np.float32(y)]])  #마우스 입력

# Update(=correction): In the second phase, it records the object's position and adjusts the covariance for the next cycle of calculations   
kalman.correct(current_measurement)

# Predict: In the first phase, the Kalman filter uses the covariance calculated up to the current point in time to estimate the object's new position
current_prediction = kalman.predict()

```

![image](https://user-images.githubusercontent.com/17797922/40174416-f9f5df64-5a0f-11e8-9c8a-cbbdec5d3412.png)

> [칼만필터.pptx](https://github.com/adioshun/gitBook_SystemSetup/files/2012933/default.pptx)

## Predict : motion\(=time\) update

* 예상 되는 정보, 현재 -&gt; 미래, 수정해서 갱신 하는 정보
* 더하기 연산\(=conv., addtional\)
* 정확도 향상이 목적이 아님
* Add more information
* Measure가 Not Available일때

## Correction : Measurement Update = correct

* 하나의 사실에 대해 모순되는 정보 있을때 \(eg. Prior와 Measure가 다를때\)
  * Prior : 내 위치라고 생각 하는 값
  * measure : 실제 내 위치
* 수행시, 공분산 낮아지고 & 정확도 향상

> 칼만 GAIN : 두 분포(예측 & 관측) 중에 가중치를 줄지 결정 ($$KG = \frac{E_{est}}{E_{est}+E_{mea}}$$)

![image](https://user-images.githubusercontent.com/17797922/40169944-36caa93c-5a02-11e8-9664-7584d9eebcd5.png)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Basic_concept_of_Kalman_filtering.svg/1701px-Basic_concept_of_Kalman_filtering.svg.png)

* Each state from the individual sensors with their respective error covariance is used for correcting the state estimate in the Kalman Filter.
* The error covariance represents the trust in the state estimation,
* e.g. a camera image is reliable for estimating the width of objects but distance or speed measurements are very inaccurate.
* In contrast a RADAR sensor provides very accurate distance and velocity measurements.
* Thus, in the final state estimate, velocity information and distance will be closer to the RADAR measurements, while the size would be closer to the measurements from the camera which, in theory, should result in a better final state estimate.

---

## 1. 정의

* Kalman filter is a scheme of estimation of signals`(=position of an Vehicle)` by combining multiple sources of **measurements** or **estimation** with uncertainties.
  * **Measurements** : The position of the object from lidar or radar.
  * **Estimation** : The prediction of the movement of the object based the understanding of the **speed** of the object.

## 2. 절차

### 2.1 절차\(간략\) `The process of combination is as follows:`

1. 대략적 위치 추정 : `Make a wild guess of the position of the object (initialization);`
2. 측정값을 활용하여 정확도 향상 : `Use the measurement of the position to improve the accuracy (update by measurement);`
3. motion prediction과 2단계에서의 업데이트된 예측값 `(updated estimation)`을 이용하여서 예측 정확도 향상 : `Use the motion prediction and based the updated estimation of the object’s position in step 2 to further predict/improve the estimation of the position of the object (predict by independent motion estimation)`
4. 3단계 결과를 이용하여 위치를 예측, 2~4단계 부터 반복 `Use the outcome of step 3, as the new estimation of the object’s position, repeat the iteration starting from step 2.`

### 2.2 절차\(상세\)

#### A. Using the step 2,

* Using the step 2, one can improve on the accuracy/certainty of the estimation of the position of the object, as the measurements are related events of observation.

#### B. Using the step 3 of object movement prediction,

* Using the step 3 of object **movement prediction**, it adds observations of the object, **independent** to the measurements of the position of the object.
* This would further reduce the dependency of the accuracy or availability of the measurements of the object’s position in step 2.

#### C. In both step2, and 3,

* 2,3단계 측정값과 예측값은 가우시간 분포로 모델링 된다.
* In both step2, and 3, the certainty of the measurements, and prediction of movement, are modeled as **Gaussian distributions**.
* The **mean of the Gaussian distribution** is the estimated value, while the variance is the representation of the certainty of the measurements/predictions.
* mean of the Gaussian distribution = 예측값
* variance = representation of the certainty of the measurements/predictions
* Gaussian distribution represents well the intuition that an estimate would have symmetry high likelihood to be around the mean.
* The extent to be closed to the mean is the degree of the certainty.

**For the step 2**,

* 측정값에 기반해 업데이트된 예측값은 아래 값들을 이용해 가중치가 적용된다. : 이전 평균`(previous mean)`의 평균`(average )` + 새 측정값의 평균
* the **updated estimation** based on **related measurement** would be the weighted **average of previous mean**, and the **mean of the new measurement**.
* 교차 가중치 평균에 대하여서는 알아 두는게 좋다. It’s especially worthy noting that it’s a **cross weighted average**, that
* the **previous estimate’s variance** is the weight of the **new measurement**’s weight,
* while the **current measurement’s variance** is the weight for the **previous estimate**.
* This would favor the new measurement, if the new measurement has smaller variance, i.e. more certain.

**For the step 3**,

* as it’s an **independent estimation**, the **new mean** and **variance** would be the **sum** of the previous estimated values \(mean, variance\) and prediction’s.
* Although this may not improve on the certainty of the overall estimation of the position, but it might help to add more information from independent source of the position of the object.
* This would be especially helpful, when the measurements may not be available, or always credible.
* In reality, it may help to improve on the accuracy of the estimation of the object’s position.

---

## 1. 정의

* 불확실한 측정값을 이용하여 미지의 값을 예측 하는것
* Kalman Filtering uses **imperfect measurements** observed over time and produces **estimates of unknown variables**

## 2. 절차

|![](https://cdn-images-1.medium.com/max/1100/1*11DTo3NRPXq_SnU0S5EHmg.png)|![](https://cdn-images-1.medium.com/max/1100/1*x1_NCZrJsBwvADPSno7YvQ.png)|
|-|-|


![](https://cdn-images-1.medium.com/max/1100/1*GQKTKlknURjgggGMlD-7_Q.png)

This algorithm is a recursive two-step process: **prediction**, and **update**.

* 예측`(prediction)`단계에서는 현재의 불확실값을 포함한 상태에서 예측`(estimates )`을 한다. `The prediction step produces estimates of the current variables along with their uncertainties.`
* 이 **예측**은 특정 모델에 기반 하는데 이 모델은 **시간의 흐름**에 따라 값이 어떻게 변화를 기록한 것이다. `These estimates are based on the assumed model of how the estimates change over time.`
* 업데이트`(update)` 단계는 다음 측정값이 observed되면 완료된다. `The update step is done when the next measurements (subject to noise) is observed.`
* 이단계에서 예측값\(=이후 State로 표기\)은 가중치 평균`(예측된 상태와 현 측정값 기반 상태의 평균)`을 통해 업데이트 된다. `In this step, the estimates (let’s call it state from here on) are updated based on the weighted average of the predicted state and the state based on the current measurement.`
* 낮은 가중치는 높은 불확실성을 의미 한다. `A lower weight is given to that with a higher uncertainty.`

![](https://cdn-images-1.medium.com/max/1100/1*QJsilpC73Afq0wurq5Ie1Q.png)

![](https://cdn-images-1.medium.com/max/660/1*2XhsE376_bgaQFNk_YQG3Q.png)

## 3. 특징

* 칼만필터는 ~~**전체 측정값**~~이 아니라 **현재의 측정값**과 **이전의 계산된 상태\(예측\)값**만 필요로 한다. `It is interesting to note that the Kalman Filter doesn’t need the whole history of past measurements and states to do its thing, it only uses the present input measurement and the previously calculated state and uncertainty.`

![](https://cdn-images-1.medium.com/max/1100/1*ejEn4kuqUW_l0b76EkTdew.png)  
![](https://cdn-images-1.medium.com/max/1100/1*fP845GoKX2B8lkHokzKRrw.png)

## 4. 구현

* I implemented an Extended Kalman Filter algorithm
* to predict the position `(px, py)` and velocity `(vx, vy)` of a moving object
* given somewhat noisy stream of measurements from a **lidar sensor**, and a **radar sensor**.
* The algorithm **fuses** these measurements.
* 가정사항 **고정된 속도**로 이동 `Along with the assumption that the object being tracked is moving at a constant velocity,`
* it produces the **state estimate \(px, py, vx, vy\)** that is more accurate than any one of the aforementioned information sources alone.

### 4.1 입력 데이터

![](https://cdn-images-1.medium.com/max/1100/1*kpaPgW_8W-viUCboVmOFGw.png)

* 라이다는 **거리**를 측정 할수 있으며 **데카르트 좌표계**로 변경 가능 하다.
* A **lidar** can measure **distance** of a nearby objects
* that can easily be converted to **cartesian coordinates** \(`px, py`\) .

* 레이다는 **속도**와 **거리**를 측정 할수 있으며 **폴라 좌표계**로 변경 가능 하다.

* A **radar** sensor can measure **speed** within its line of sight \(drho\)using something called a doppler effect. It can also measure **distance** of nearby objects
* that can easily be converted to **polar coordinates** \(`rho, phi`\) but in a lower resolution than lidar.

* 데카르트 좌표계와 폴라 좌표계는 상호 변환 가능 핟. `You can easily convert values from cartestian to polar coordinate systems and vice versa.`

| ![](https://cdn-images-1.medium.com/max/1100/1*0-HFGJPA8EPoFJ5lSLnDbg.png) | ![](https://cdn-images-1.medium.com/max/1100/1*Jlw52x7LnqJ1-wppEJekIQ.png) |
| --- | --- |


---

![image](https://user-images.githubusercontent.com/17797922/40119558-f7ebf0cc-5957-11e8-8aa4-a6570d70876f.png)

## 1. Kalman Filters

> 출처 : [UDACITY SDCE Nanodegree Term 2: Kalman Filters for Sensor Fusion](https://medium.com/@ckyrkou/udacity-sdce-nanodegree-term-2-kalman-filters-for-sensor-fusion-1dde97ea628b)

* 원래 칼만 필터는 연속된 측정값에서 모르는 변수들을 예측\(estimates\) 할때 사용 한다. `The traditional Kalman Filter is an algorithm that is used to produce estimates for unknown variables given a series of measurements.`

* Bayesian inference을 이용하여 변수들의 결합확률분포 예측한다. `It uses Bayesian inference to estimate a joint probability distribution over the variables for a considered period.`

* 본질적으로 칼만필터는 변수들을 예측 하기 위해 **mean vector** 와 **co-variance matrix**를 유지 하고 있는다.`Essentially, the Kalman Filter maintains a mean vector and co-variance matrix for the estimated variables`

* that represent the belief for each possible state through Gaussian functions.

* 이 알고리즘과 변종들`(Extended and Unscented)`은 다음 두 주기 동안 반복된다. `The algorithm and its variants (Extended and Unscented Kalman Filters) iterate on two main cycles:`

* Measurement Update : In the measurement update step we use new observations from the sensors to update our belief estimation for the unkown variables.
* State Prediction. : Then in the state prediction step we predict using a system model \(e.g., motion model\) the future value of the unknown variables.

![](https://i.imgur.com/I7ymTir.png)

* 멀티센서일때는 각 센서 마다 고유의 measurement update scheme가 있다. `In the case where multiple sensors are used then each sensor has its own measurement update scheme.`

* 멀티 센서여도 The belief about the state of the unkown variables is updated asynchronously each time the measurement is received regardless of the sources sensor.

### 1.2 Extended Kalman Filters \(EKF\)

* 기본 칼만필터의 단점\(drawback\)은 it assumes a linear measurement model and state prediction model.
* 라이다\(LiDar\) 센서 has a linear measurement update model
* 레이더\(Radar\) 센서 has a non-linear update model.

* 확장 칼만필터로 해결 가능 `The Extended Kalman Filter attempts to solve such problems`

* by linearizing the non-linear state transition functions using Taylor Expansion around the mean location of the original function.
* In addition, the linearization requires that the **Jacobian** of the state transition is computed.

### 1.3 Unscented Kalman Filters \(UKF, 분산점칼만필터\)

* 분산점 칼만필터를 이용하여서 **non-linear**현상을 좀더 정확히 모델링 할수 있다. `With Unscented Kalman Filters we are able to accurately model non-linear phenomena.`

* EKF의 **linearizing** 방법 대신, UKF는 **unscented transformatio**를 사용 한다. `Instead of linearizing a non-linear function, UKF uses the unscented transformation to approximate the belief probability distribution.`

* UKF방법은 linearization 보다 성능도 좋고, **Jacobians**연산도 안하게 된다. `In this way it performs better than linearization and does not require to compute Jacobians.`

#### A. 개요

* UKF의 핵심은 **다변량 가우스 분포**`(Multivariate Gaussian distribution)`를 찾는 것이다. `The main jist(point) of UKF is to find the multivariate Gaussian distribution that approximated the real belief distribution.`

* predicted states가 정규분포`(normaly distributed)`가 아닐수 있지만 UKF는 그렇다고 가정한다. `The predicted states may not be normaly distributed but the UKF assumes that they are.`

* Specifically, the Gaussian distribution approximated the real distribution as close as possible with respect to its mean and covariance matrix.

#### B. pipeline

* The pipeline for UKF is to
* first generate some **samples sigma points** that define the Gaussian.
* Then to predict **new sigma points** based on the system model \(e.g., motion model\).
* Using the new sigma points we then **predict the mean and covariance of the Gaussian**.

* These three steps constitute the **Prediction Step** for the UKF.

* The **Measurements Update** follows next,

* which includes Predicting the new measurements and updating the state belief.

### 1.4 칼만-부시 필터\(The Kalman–Bucy filter\)

칼만 필터의 연속 시간 버전이다.

---

## 추천 강의

![image](https://user-images.githubusercontent.com/17797922/40107264-bb9a86e4-5932-11e8-8d47-aa0ed5aef6ef.png)

[중등2 - AI for Robotics\(Stanford\)](https://www.youtube.com/playlist?list=PLlSZlNj22M7RJ_6BW8w699SucNXzZZo83): Youtube, 쥬피터 강사, 2017

[중등4 - Introduction to AI\(Stanford\)](https://www.youtube.com/playlist?list=PLlSZlNj22M7RtNfjq94w2m4E9U4Y1sAG5): 파티클 필터 , 쥬피터

## Particle filter

-[Particle Filter Explained without Equations](https://www.youtube.com/watch?v=aUkBa1zMKv4):youtube 7:30초

![](https://cdn-images-1.medium.com/max/800/1*s2kA7oclIHoCAQsao2fXhw.jpeg)

![image](https://user-images.githubusercontent.com/17797922/40173698-a45fd8ae-5a0d-11e8-8e37-681f95210626.png)


---

칼만 필터를 사용하면서도 칼만 게인이 어떤 의미인지 잘 모르겠고,

SLAM과의 관계가 궁금하다면 다음 글들을 한 번 읽어보세요.

http://refopen.blogspot.kr/2014/08/blog-post_19.html
http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and.html
http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and_21.html
http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and_24.html
[출처] Kalman gain 해석 (OpenCV KOREA 대한민국 최고의 컴퓨터비젼 커뮤니티) |작성자 refopen
