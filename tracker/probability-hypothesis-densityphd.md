# [Effective Data Association Algorithms for Multitarget Tracking](https://macsphere.mcmaster.ca/bitstream/11375/16272/2/thesis%20-%20Biruk%20Habtemariam.pdf)

### 2.5 Random Finite Set Methods

The Probability Hypothesis Density (PHD) filter [10][11][89] is a Bayesian multitarget tracking estimator initially proposed in [56]. 

The PHD filter is developed based on the 
- Random Finite Set (RFS) theory, 
- point processes, and 
- Finite Set Statistics (FISST).

특징 : It estimates all the targets states at once, as a multitarget state, projected on the single-target space.

The PHD filter has been shown an effective way of tracking a time-varying multiple number of targets that avoids model-data association problems [56]. 

변형/개선  
- A Gaussian mixture implementation of PHD filter (GM-PHD) is presented in [89]. 
- For nonlinear measurements, the Sequential Monte Carlo (SMC) implementation of the PHD filter is presented in [10].


---

### 4.2 GM-PHD 필터

Data Associateion까지 고려한 다중 객체 추적에 적용

이전 프레임의 포인트를 현재 프레임의 물체에 자동으로 누적하여 물체 해상도 및 보행자 분류 성능을 향상

```
이연주, 서승우, "GM-PHD 필터를 이용한 보행자 탐지 성능 향상 방법", 서울대, 2015
```


---