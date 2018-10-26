
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

However, this result requires that the mean ofthe initial state estimate is equal to the mean of the initialstate, and its associated error covariance matrix is equal tothe true initial covariance. 

In practice, this is rarely thecase. 

Ideally, any initial transients introduced by incorrectinitialization will quickly be eliminated, but this cannot beguaranteed. 

The effect of such errors on Kalman filters forgeneral problems have been examined in [3 − 5] and morerecently, with a focus on target tracking, in [6].There are additional factors to be considered for targettracking problems. 

In real-world radar tracking problems,the measurements are range and azimuth in the 2D case,and range, azimuth, and elevation in the 3D case. 

Unbiasedposition measurements and associated measurement covari-ances can be derived from these radar measurements [7] , butthe associated measurement errors are no longer Gaussian.For the ground target tracking problem using the groundmoving target indicator (GMTI) radar sensor, the 3D posi-tion of a target can be estimated using the GMTI range andazimuth measurements, sensor position, and terrain data [8] .A similar situation occurs in the video tracking problem.The 3D position of a ground target can be estimated usingthe target centroid pixel location, intrinsic and extrinsiccamera parameters, and terrain data [9] . 

Similarly, the er-rors in the 3D position estimate of the target for the GMTIand video tracking problems are not Gaussian. 

This lack ofGaussianity will also have an impact on the performance ofthe filter and can potentially exacerbate any initializationerrors. 

This is demonstrated in [10], which considers theproblem of target tracking with long range radars.In this paper, we compare two track initiation algo-rithms, the single-point (SP) method [11−12] and the two-point difference (TPD) method [2] , using position-only mea-surements in 1D, 2D, or 3D. 

We assume that the targetmotion is described by the nearly constant velocity model(NCVM) [2] . 

Then, the SP algorithm initiates the trackusing the first position measurement and sets the veloc-ity components to zero. 

The maximum possible speed ofthe target is used, in addition to the measurement covari-ances, to initialize the associated covariance matrix [11−12] .A KF is then used to process subsequent position measure-ments. 

In contrast, the TPD algorithm [2] uses informationon the first two measurements alone to initialize the filter.This estimate represents the maximum likelihood estimatefor Gaussian position errors. 

We demonstrate numericallythat the SP method has a smaller mean square error ma-trix (MSEM) than the TPD for a 3D radar target trackingproblem. 

We conjecture that this result holds analytically.We analytically show that, if the process noise approacheszero and the maximum speed of a target used to initial-ize the velocity variance approaches infinity, then the SPalgorithm reduces to the TPD algorithm.The organization of the paper is as follows. 

Section 1 de-scribes the target dynamic and measurement models. 

Sec-tion 2 presents the SP and TPD track initiation algorithms.The bias and the MSEM of the two estimators at the sec-ond observation time are discussed in Section 3. 

Section 4establishes the relationship between the two track initiationalgorithms analytically. 

Finally, Sections 5 and 6 presentnumerical results and conclusions.Let n (1, 2 or 3) denote the dimension of the targetposition. 

We use I and 0 n to represent the n × n identitymatrix and null matrix, respectively. 

A general m × n nullmatrix is denoted by 0 m×n .