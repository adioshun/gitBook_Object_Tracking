|논문명 |Model Based Vehicle Tracking for Autonomous Driving in Urban Environments |
| --- | --- |
| 저자\(소속\) | Anna Petrovskaya\(스탠포드\) |
| 학회/년도 | 2008, [논문](http://www.roboticsproceedings.org/rss04/p23.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | [홈페이지](https://cs.stanford.edu/people/petrovsk/uc.html), [포스터](https://cs.stanford.edu/people/petrovsk/dn/publications/anya_rss08_tracking_poster.pdf)] |
| 코드 | - |


|년도|1st 저자|논문명|코드|
|-|-|-|-|
|2008|Anna Petrovskaya|[Model Based Vehicle Tracking for Autonomous Driving in Urban Environments](https://cs.stanford.edu/people/petrovsk/dn/publications/anya_rss08_tracking.pdf)|-|
|2009|Anna Petrovskaya|[Model Based Vehicle Tracking in Urban Environments.](https://cs.stanford.edu/people/petrovsk/dn/publications/anya_icra09_tracking.pdf)|-|
|2009|Anna Petrovskaya|[Model Based Vehicle Detection and Tracking for Autonomous Urban Driving](https://cs.stanford.edu/people/petrovsk/dn/publications/anya_auro09_tracking.pdf)|-|
|2012|Anna Petrovskaya|[Awareness of Road Scene Participants for Autonomous Driving](https://cs.stanford.edu/people/petrovsk/dn/publications/anya-datmo-handbook2012.pdf)|-|



# Model Based Vehicle Tracking for Autonomous Driving in Urban Environments

Our approach
- models both **dynamic** and **geometric** properties of the tracked vehicles and
- estimates them using a **single Bayes filter** per vehicle.

We also show how to build efficient **2D representations** out of 3D range data and how to detect poorly visible black vehicles.

## I. INTRODUCTION

기존 Tracking 연구들
- Typically these approaches perform **data segmentation** and **data association** prior to performing a **filter update**.
- Usually only **position** and **velocity** of each vehicle are tracked.
- The vehicle tracking literature almost universally relies on variants of **Kalman filters**, although particle filters and hybrid approaches have been widely used in other tracking applications [8, 9, 10].

```
[8] D. Schulz, W. Burgard, D. Fox, and A. Cremers. Tracking multiple moving targets with a mobile robot using particle filters and statistical data association. In ICRA, 2001.
[9] S. S. Blackman. Multiple hypothesis tracking for multiple target tracking. IEEE AE Systems Magazine, 2004.
[10] S. S¨arkk¨a, A. Vehtari, and J. Lampinen. Rao-blackwellized particle filter for multiple target tracking. Inf. Fusion, 8(1), 2007.
```

본 연구와 기존 연구의 차이점


- we propose a **model based** approach which encompasses both **geometric** and **dynamic** properties of the tracked vehicle in a **single Bayes filter**.
  - To properly model the dependence between geometric and dynamic vehicle properties, we introduce **anchor point coordinates**.


- we introduce an abstract sensor representation we call the **virtual scan**, that allows for efficient computation and can be used for a wide variety of laser sensors.


- We present techniques for building virtual scans from 3D range data and show how to detect poorly visible black vehicles in laser scans.


## II. REPRESENTATION

### A. Probabilistic model and notation

이론적측면에서 추적은 **Single joint probability distribution over the state parameters** 이다. `From the theoretical standpoint, multiple vehicle tracking entails a single joint probability distribution over the state parameters of all of the vehicles. `

하지만 이런 representation은 현실적이지 못하다. 왜냐하면 차량이 증가하면 추적불가 현상이 빈번히 발생 하기 때문이다. `Unfortunately, such a representation is not practical because it quickly becomes intractable as the number of vehicles grows. `

또한, 전체 차량의 수도 알수 없다. `Also, since the number of vehicles is unknown and variable, it is in fact challenging to model the problem in this way. `

연구를 통해 차량간의 위존(=dependencies)성은 두 차량이 가까우면 커지고 멀면 작아 지는것을 알게 되었다.  `We note that dependencies between vehicles are strong when vehicles are close together, but become extremely weak as the distance between vehicles increases.`

따라서 서로 멀리 떨어진 차량의 디펜던시를 모델링 하는건 불필요 하다. `Hence it is wasteful to model dependencies between vehicles that are far from each other.`


대신에, Instead, we will
- represent **each vehicle** with a **separate Bayesian filter**, and
- represent **dependencies between vehicles** via a set of **local spatial constraints**.

특별히, 여러 assumption을 두었다. `Specifically we will assume that`
- no two vehicles overlap,
- that there is a free space of at least 1m around each vehicle and
- that all vehicles of interest are located on or near the road.


This representation is efficient because its complexity grows linearly with the number of vehicles. It also easily accommodates a variable number of tracked vehicles.

For each vehicle we estimate
- its 2D position and orientation $X_t = (x_t, y_t, θ_t)$ at time `t`,
- its forward velocity $v_t$ and
- its geometry G.

Also at each time step we obtain a new measurement $Z_t$.


![](https://i.imgur.com/8KCiSf3.png)

See Fig. 2 for a dynamic Bayes network representation of the resulting probabilistic model.

The dependencies between the parameters involved are modeled via probabilistic laws discussed in detail in Sects. II-C and II-E.

- 속도 : For now we briefly note that the velocity evolves over time according to **$p(v_t \mid v_{t-1})$**

- 이동 모델 : The vehicle moves based on the evolved velocity according to a dynamics model: **$p(X_t \mid X_{t-1}, v_t)$**

- 측정 모델 : The measurements are governed by a measurement model: **$p(Z_t \mid X_t, G)$**

- 특정 시간의 이동 경로 : For convenience we will write **$X_t = (X_1,X_2, ...,X_t)$** for the vehicle’s trajectory up to time `t`.

- 특정 시간에서의 모든 측정 속도, 측정 값 : Similarly, **$v_t$** and **$Z_t$** will denote all velocities and all measurements up to time `t`.

### B. Vehicle geometry

차량을 정확히 모델링 하는것은 복잡하다. `The exact geometric shape of a vehicle can be complex and difficult to model precisely. `


이를 간단히 하기 위해 `넓이 x 길이`만 가지고 사각형(`W x L`)으로 정의 하였다. `For simplicity we approximate it by a rectangular shape of width W and length L. `
  - 2D로 표현해도 충분하다, 높이 정보(H)는 자율주행에서는 불필요하다. `The 2D representation is sufficient because the height of the vehicles is not important for driving applications. `

차량추적에서 차량의 중심 위치를 추적하는것이 일반적이다. `For vehicle tracking it is common to track the position of a vehicle’s center within the state variable $X_t$. `

![](https://i.imgur.com/r9bWpv4.png)

하지만, 우리의 생각과 차량의 모양/위치에는 흥미로운 연관 관계가 있다. `However, there is an interesting dependence between our belief about the vehicle’s shape and position (Fig. 3). `

As we observe the object from a different vantage point, we change not only our belief of its shape, but also our belief of the position of its center point.

Allowing $X_t$ to denote the center point can lead to the undesired effect of obtaining a non-zero velocity for a stationary vehicle, simply because we refine our knowledge of its shape.

이 문제를 해결하기 위해 `To overcome this problem`, we view $X_t$ as the pose of an anchor point who’s position with respect to the vehicle’s center can change over time.

1. Initially we set the anchor point to be the center of what we believe to be the car shape and thus its coordinates in the vehicle’s local coordinate system are C = (0, 0).

2. We assume that the vehicle’s local coordinate system is tied to its center with the x-axis pointing directly forward.

3. As we revise our knowledge of the vehicle’s shape, the local coordinates of the anchor point will also need to be revised accordingly to C = (Cx, Cy).

따라서, 최종 G는 다음과 같다. `Thus the complete set of geometric parameters is` **$G = (W, L, C_x, C_y)$**.

### C. Vehicle dynamics model

차량 속도 : Given a vehicle’s velocity $v_{t−1}$ at time step ${t−1}$,

the velocity evolves via
- addition of random bounded **noise** based on maximum allowed acceleration $a_{max}$ and
- the time delay $\Delta t$ between time steps ${t−1}$ and $t$.
- Specifically, we sample $\Delta v$ uniformly from $[−a_{max}\Delta t, a_{max}\Delta t]$.

차량 포즈 :

The pose evolves via linear motion - a motion law that is often utilized when exact dynamics of the object are unknown.

The motion consists of perturbing(교란, 동요) orientation by $∆θ1$, then moving forward according to the current velocity by $vt\Delta t$, and making a final adjustment to orientation by $\Delta \theta_2$. Again we sample $\Delta \theta_1$ and $\Delta \theta_2$ uniformly from $[−d\theta_{max}∆t, d\theta_{max}\Delta t]$ for a maximum allowed orientation change $d \theta_{max}$.




### D. Sensor data representation

최근 라이더 센서 성능이 좋아져서 충분한 성능이 나온다.

몇가지 요소들이 센서데이터 활용을 비효율적으로 하고 있다. `A number of factors make the use of raw sensor data inefficient.`

- 차량의 이동으로 매 수집되는 데이터는 vantage point이다. `As the sensor rotates to collect the data, each new reading is made from a new vantage point due to ego-motion. `

- 이 점을 무시 한다면, 센서데이터에는 많은 노이즈가 포함된다. `Ignoring this effect leads to significant sensor noise. `

- 이 점을 고려 한다면, 관심영역과 관련있는 데이터에 빠르게 access하는것을 어렵게 한다. `Taking this effect into account makes it difficult to quickly access data that pertains to a specific region of space. `

- 수집되는 센서 데이터의 대부분은 땅, 나무, 처럼 차량 추적에 불필요한 데이터 이다. `Much of the data comes from surfaces uninteresting for the purpose of vehicle tracking, e.g. ground readings, curbs and tree tops. `

- 마지막으로, 차량은 지표면에 제한적으로 이동하는 2D 이므로 3D 데이터 처리는 많은 자원 소모를 가져 온다. `Finally, the raw 3D data wastes a lot of resources as vehicle tracking is a 2D application where the cars are restricted to move on the ground surface. `

따라서, 데이터를 전처리 하여서 차량 추적에 맞추어서 처리 하는게 필요 하다. `Therefore it is desirable to pre-process the data to produce a representation tailored for vehicle tracking.`

![](https://i.imgur.com/uW9mbGe.png)

빠른 처리를 위해서 본 논문에서는 polar coordinates로 그리드를 생성하였다. `To expedite computations, we construct a grid in polar coordinates - a virtual scan - which subdivides 360◦ around a chosen origin point into angular grids (Fig. 4). `
  - 즉, a virtual scan - which subdivides 360◦ around a chosen origin point into angular grids

각 angular grid에는 가까운 물체의 range 정보(`free, occupied, and occluded`)를 저장 한다. `In each angular grid we record the range to the closest obstacle. Hence each angular grid contains information about free, occupied, and occluded space.``

We will often refer to the cone of an angular grid from the origin until the recorded range as a ray due to its similarity to a laser ray.

Virtual scans simplify data access by providing a single point of origin for the entire data set, which allows constant time look-up for any given point in space.

As we mentioned earlier it is important to compute correct world coordinates for the raw sensor readings.

However, once the correct positions of obstacle points have been computed, adjusting the origin of each ray to be at the common origin for the virtual scan produces an acceptable approximation.

Constructed in this manner a virtual scan provides a compact representation of the space around the ego-vehicle classified into free, occupied and occluded.

The classification helps us properly reason about what parts of an object should be visible as we describe in Sect. II-E.

For the purpose of vehicle tracking it is crucial to determine what changes take place in the environment over time.

With virtual scans these changes can be easily computed in spite of the fact that ego-motion can cause two consecutive virtual scans to have different origins.

The changes are computed by checking which obstacles in the old scan are cleared by rays in the new scan and vice versa.

This computation takes time linear in the size of the virtual scan and only needs to be carried out once per frame.

![](https://i.imgur.com/0J6NYAN.png)

Fig. 4(d) shows results of a virtual scan differencing operation with
- red points denoting new obstacles,
- green points denoting obstacles that disappeared, and
- white points denoting obstacles that remained in place or appeared in previously occluded areas.

### E. Measurement model Given
