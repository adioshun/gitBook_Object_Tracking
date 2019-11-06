# Probabilistic data association

the PDAF takes an expected value, which is the minimum mean square error (MMSE) estimate

- IPDAF : PDAF를 기반으로 트랙 존재 확률 개념을 추가 
- IMM-PDAF : 다중의 모델을 정의하고 각 모델의 가중치를 고려하여 상태를 추정 하는 IMM(Interacting Multiple Model)와 연계 


추적에 활용 방안 : 칼만필터의 갱신 단계에서 어떤 측정치를 사용하여 상태를 갱신 할지 결정하는 데이터 연관 기법은 IPDAF를 사용 



---

- the PDAF updates the track with a **weighted average** of all validated measurements

- The weights are the individual association probabilities


---
# [Effective Data Association Algorithms for Multitarget Tracking](https://macsphere.mcmaster.ca/bitstream/11375/16272/2/thesis%20-%20Biruk%20Habtemariam.pdf)


#### 2.3.1 Probabilistic Data Association

The Probabilistic Data Association Filter (PDAF) [15] [14], also referred as the all-neighbors data association filter [19], implements a Bayesian approach for data association. 

In PDAF, weights are assigned to the measurements based on probabilistic inference made on the number of measurements and location of the measurements relative to the predicted track state [14]. 

For example, for the scenario in Figure 2.2 each validated measurement, i.e., {z1(k), z2(k), z3(k)}, is assigned a weight in contrast to choosing a single measurement as in NNF and SNF methods. 

Track state is updated with the innovations from each measurements are combined according to the assigned weights. 

Whenever there are multiple targets close to each other, joint association events can be considered in order to resolve from which target a measurement is originated uncertainty as in Joint Probabilistic Data Association Filter (JPDA) [23][20]. 

The PDAF as well as its multitarget variant, JPDAF, assume that track/tracks are already uninitialized. 

Tracks can be initialized, for example, with two-point track initialization method [14]. 

Furthermore, in a more robust approach, target existence models can be incorporated into the PDA framework as in Integrated Probabilistic Data Association Filter (JIPDA) [28] and similarly to the JIPDA framework as in Joint Integrated Probabilistic Data Association Filter (JIPDA) [57]. 

With target existence model, the JIPDA handles time varying number of targets and track management tasks such as track initiation, confirmation and deletion.







---

- [[매거진(추천)] The Probabilistic Data Association Filter](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.212.383&rep=rep1&type=pdf): gitPaper Tracking 정리 참고 

