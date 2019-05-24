

본 논문에서는 앞서 언급한 문제를 극복하고자 확률밀도가정(Probability Hypothesis Density (PHD))필터를 이용하여 영
상기반의 온라인 다중객체추적을 구현한다. 

PHD 필터는 다중 객체와 측정치들을 Random Finite Set에 근거하여 객체 집합과 관측치 집합으로 모델링한다. 

기존의 데이터연관 기반의 추적 방식들과 다르게 PHD 필터는 각 객체를 독립적으로 추정하기 보다 객체들을 하나의 집합으로 고려하여 추정한다. 

이러한 특징 때문에 각 객체에 하나의 관측지를 할당하는 **데이터연관 부분이 불필요**하다. 

또한, PHD 필터는 객체의 사라짐, 출현, 그리고 검출 불확실성을 확률적으로 모델링하여 표적 객체 관리와 검출 불확실성 관리를 필터링 과정에서 자동적으로 처리할 수 있다는 장점이 있다.

---

# [Multi-target Tracking with PHD Filters](https://www.math.u-bordeaux.fr/~mpace/PhdFiltering.html)

## 분류 

Random Finite Set (RFS)기반 기법들 
- Multiple Hypotheses tracking (MHT)
- Joint Probabilistic Data Association Filter (JPDAF) 
- (PMHT) Probabilistic MHT 

RFS기반 기법 특징 : is based on the Random Finite Set (RFS) formulation in which the collection of individual targets is treated as a set-valued state and the collection of observations as a set-valued observation.

joined with Mahler's finite set statistics (FISST)기법 
- This approach, joined with Mahler's finite set statistics (FISST), has lead to the development of an effective class of multiple-target filters such as the Probability Hypothesis Density (PHD) filters.

대표적인 두가지 예) You can find here some example of the application of two approximations of the PHD recursion: 
- a Sequential Monte Carlo PHD filter (SMC-PHD) and 
- a Gaussian Mixture PHD filter (GM-PHD) to a realistic naval and aerial scenario.

## PHD Filters

The Probability Hypothesis Density (PHD) filter is a multiple-target filter for recursively estimating the number and the state of a set of targets given a set of observations. 

It is able to operate in environments with false alarms and miss-detections and it works by propagating in time the intensity of the targets RFS instead of the full multi-target posterior density.

In literature, various implementations have been proposed and their performance compared using different levels of clutter and model uncertainty. 


### SMC-PHD

The generic sequential Monte Carlo implementation (SMC-PHD) filter, proposed by Vo et al. in [4], generally suffers of an high computational cost as it requires a large number of particles and relies on clustering techniques to provide state estimates. 

The unreliability of estimates due to inaccuracy introduced by the clustering step and the computational complexity constitute its main drawbacks. 


> Python Particle Probability Hypothesis Density Filter: B.-N. Vo, S. Singh, and A. Doucet, “Sequential Monte Carlo implementation of the PHD filter for multi-target tracking,”, 2003

### 예 2 : GM-PHD

To alleviate these problem a closed form solution to the PHD filter recursion, called Gaussian Mixture PHD (GM-PHD), has been proposed by Vo and Ma in [7]. 

This approach does not require clustering procedures but, since it makes use of the Kalman filter equations, it is restricted to linear-Gaussian target dynamic. 

When targets show a mildly non-linear dynamic it is generally possible to rely on extensions for the GM-PHD filter using the Extended Kalman filter (EK-PHD) or the Unscented Kalman filter (UK-PHD) or to use the Gaussian Particle Implementations of the PHD filter.




> [GM-PHD 필터를 이용한 보행자 탐지 성능 향상 방법](http://www.dbpia.co.kr/Article/NODE06594856), 2015


[GM-PHD filter implementation in python (Gaussian mixture probability hypothesis density filter)](https://github.com/danstowell/gmphd): N. Vo and W. K. Ma. The gaussian mixture probability hypothesis density filte, 2006
- 설명 : http://www.mcld.co.uk/blog/2013/update-on-gm-phd-filter-with-python-code.html
- [GMPHD-py with its application to underwater robotic mapping](https://github.com/tfabbri/gmphd-py)



