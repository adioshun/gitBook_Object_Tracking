## [Tracking in Several Real-World Scenarios](https://opencommons.uconn.edu/cgi/viewcontent.cgi?referer=https://www.google.co.kr/&httpsredir=1&article=7382&context=dissertations), 2016, 156p

- Two-point differencing using the unbiased measurement conversion from polar to Cartesian coordinates was used in the initialization of the other filters[7].

```
[7] Y. Bar-Shalom, X.-R. Li, and T. Kirubarajan, Estimation with Applications to Tracking and Navigation. New York: Wiley, 2001.
```

---

# Comparison of Single-point and Two-point Difference Track Initiation Algorithms Using Position Measurements

> MALLICK Mahendra, 2008 [[Download]](https://www.researchgate.net/publication/245568628_Comparison_of_Single-point_and_Two-point_Difference_Track_Initiation_Algorithms_Using_Position_Measurements)

- 트랙초기화(Track initiation)는 추적의 필수 요소이지만 중요성에 비해 연구가 많이 이루어 지지 않았다. `Track initiation is an essential component of all tracking algorithms, but one that has received little attention.`


- 움직임이 일정한 물체의 추적에는 칼만필터를 사용하는것이 일반적으로 좋다. `For situations where the dynamic and measurement models are linear and appropriate Gaussianity and independence assumptions hold, it is well-known that the Kalman filter (KF) is optimal in the minimum mean squared error sense [1−2].`


- 하지만 이런 좋은 결과를 위해서는 요구 사항들이 있다. `However, this result requires that`
- the mean of the initial state estimate is equal to the mean of the initial state,
- and its associated error covariance matrix is equal to the true initial covariance.


- 실제 적용시에는 이상적으로는 잘못된 초기화도 수정(=제거)되지만 이를 보장 할수는 없다. `In practice, this is rarely the case. Ideally, any initial transients introduced by incorrect initialization will quickly be eliminated, but this cannot be guaranteed.`

- 이러한 에러의 영향에 대한 연구가 [3-5]에서 이루어 졌고 최근에는 타겟 추적에 초점을 연구 되었다[6]. `The effect of such errors on Kalman filters for general problems have been examined in [3 − 5] and more recently, with a focus on target tracking, in [6].`

타겟 추적 문제와 관련된 몇가지 고려 사항들이 더 있다. `There are additional factors to be considered for target tracking problems.`

- 실생활에서 Radar 추적의 측정치는 2D에서는 거리, 방위각이며, 3D에서는 거리, 방위가, 고도이다. `In real-world radar tracking problems,the measurements are range and azimuth in the 2D case,and range, azimuth, and elevation in the 3D case. `

- Unbiased position measurements and associated measurement covariances can be derived from these radar measurements [7] ,
- but the associated measurement errors are no longer Gaussian.

- For the ground target tracking problem using the ground moving target indicator (GMTI) radar sensor,
- the 3D position of a target can be estimated using the GMTI range andazimuth measurements, sensor position, and terrain data [8] .
- 비디오 추적문제에서도 비슷한 상황이 발생 한다. `A similar situation occurs in the video tracking problem.`

The 3D position of a ground target can be estimated usingthe target centroid pixel location, intrinsic and extrinsic camera parameters, and terrain data [9] .

Similarly, the errors in the 3D position estimate of the target for the GMTI and video tracking problems are not Gaussian.

- 이런 비가우시안 속성으로 인해서 필터 성능에 영향을 미치고 잠재적으로 초기에러 확산을 야기 한다. `This lack of Gaussianity will also have an impact on the performance of the filter and can potentially exacerbate any initialization errors. `
- [10]에서 이를 증빙하였다.
This is demonstrated in [10], which considers the problem of target tracking with long range radars.


본 논문에서는 두개의 트랙 초기화 알고리즘을 비교 하였다. `In this paper, we compare two track initiation algorithms,`
- the single-point (SP) method [11−12] and
- the two-point difference (TPD) method [2] , using position-only measurements in 1D, 2D, or 3D.

본 논문에서는 타겟의 움직음은 고정된 속도라고 가정 하였다. `We assume that the target motion is described by the nearly constant velocity model(NCVM) [2] . `

- SP: Then, the SP algorithm initiates the track using the first position measurement and sets the velocity components to zero.
- The maximum possible speed of the target is used, in addition to the measurement covariances, to initialize the associated covariance matrix [11−12] .
- A KF is then used to process subsequent position measurements.

- TDP : In contrast, the TPD algorithm [2] uses information on the first two measurements alone to initialize the filter.
- This estimate represents the maximum likelihood estimatefor Gaussian position errors.

We demonstrate numerically that the SP method has a smaller mean square error matrix (MSEM) than the TPD for a 3D radar target tracking problem.

We conjecture that this result holds analytically.

We analytically show that, if the process noise approaches zero and the maximum speed of a target used to initialize the velocity variance approaches infinity, then the SP algorithm reduces to the TPD algorithm.

