# 칼만필터 발전 

## 1. KF

The Kalman filter (KF) is a popular choice for estimating motion in robotics. Since position information is linear, standard Kalman filtering can be easily applied to the tracking problem without much difficulty.
However, most robotic motions also contain nonlinearity requiring a modification to the KF.

## 2. EKF

The extended Kalman filter (EKF) provides this modification by linearizing all nonlinear models (i.e., process and measurement models) so the traditional KF can be applied.

Unfortunately, the EKF has two important potential drawbacks. First, the derivation of the Jacobian matrices, the linear approximates to the nonlinear functions, can be complex causing implementation difficulties. Second, these linearizations can lead to instability if the time-step intervals are not sufficiently small.

## 3. UKF

To address these limitations, the unscented Kalman filter (UKF) was developed. The UKF operates on the premise that it is easier to approximate a Gaussian distribution than it is to approximate an arbitrary nonlinear function. Instead of linearizing using Jacobian matrices, the UKF using a deterministic sampling approach to capture the mean and covariance estimates with a minimal set of sample points.
The UKF is a powerful nonlinear estimation technique and has been shown to be a superior alternative to the EKF in a variety of applications.


> 세개의 칼만필터 분석 : `A Comparison of Unscented and Extended Kalman Filtering for Estimating Quaternion Motion.`


## 추천 강의

![image](https://user-images.githubusercontent.com/17797922/40107264-bb9a86e4-5932-11e8-8d47-aa0ed5aef6ef.png)

- [중등2 - AI for Robotics\(Stanford\)](https://www.youtube.com/playlist?list=PLlSZlNj22M7RJ_6BW8w699SucNXzZZo83): Youtube, 쥬피터 강사, 2017

- [중등4 - Introduction to AI\(Stanford\)](https://www.youtube.com/playlist?list=PLlSZlNj22M7RtNfjq94w2m4E9U4Y1sAG5): 파티클 필터 , 쥬피터

- [[추천] 쥬피터 모음](https://github.com/balzer82/Kalman)


# 표윤석, ROS 로봇 프로그래밍, 349page 참고 

---

- 칼만 필터를 사용하면서도 칼만 게인이 어떤 의미인지 잘 모르겠고,SLAM과의 관계가 궁금하다면 다음 글들을 한 번 읽어보세요.
    - http://refopen.blogspot.kr/2014/08/blog-post_19.html
    - http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and.html
    - http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and_21.html
    - http://refopen.blogspot.kr/2014/08/slamsimultaneous-localization-and_24.html



- [How a Kalman filter works, in pictures](http://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)
