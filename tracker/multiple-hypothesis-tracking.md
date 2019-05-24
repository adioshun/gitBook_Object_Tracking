# Multiple Hypothesis Tracking

- 'Spatially Indexed Clustering for Scalable Tracking of Remotely Sensed Drift Ice', 2017 [[코드-Python]](https://github.com/jonatanolofsson/mht)

- [[코드-C]](https://github.com/WeatherGod/MHT)

- C. Kim, "[Multiple Hypothesis Tracking Revisited](https://ieeexplore.ieee.org/document/7410890)", ICCV 2015 , [[코드-Python]](https://github.com/jperdomo23/openmht)


- [MULTIPLE OBJECT TRACKING WITH MHT](http://www.deepvisionconsulting.com/multiple-object-tracking-with-mht/) : blog 2018



---

# [LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf): 2012, 석사 학위 논문

현 (하나의)프레임에서 바로 할당작업을 진행하는 방식과는 달리, MHT는 불확실한 상황이 되면 할당작업을 미루고 여러개의 alternative data association hypotheses를 생성 한다. ` Instead of considering just the information of one frame, Multiple Hypothesis Tracking (MHT) is a multi-scan deferred decision logic tracking algorithm that keeps multiple alternative data association hypotheses whenever the ambiguity situation occurs. `

JPDA에서 이러한 가설치(hypotheses)들을 합치는 방식 대비, MHT에서는 가설치들이 전파되어서 가장 높은 posteriors를 가지는 값만 반환된다. `Rather than combining these hypotheses in JPDA method, all the hypotheses are propagated and the one with highest posteriors is returned as solution.`

모든 track들이 유지 되기 때문에 **모션모델**이 불확실한곳에서 유용한다. ` Since all potential tracks are maintained and updated, this method is very useful when the target motion model is unpredictable.`

단점으로 시간이 지남에 따라 유지해야 하는 가설치가 기하 급수적으로 증가하긴 하지만 아직많이 사용되고 있다. [26,28,63]에서는 가설치 삭제 방안도 제시 되었다. ` Although the number of hypothesis may grow exponentially over time, MHT is still applied in many multi-object tracking systems, supplementary with hypothesis deleting mechanism [26, 28, 63]. Wang, et al. also implemented this method on Navlab for real-time road tests (see the previous Figure 2.9).`