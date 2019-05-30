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

