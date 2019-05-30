# Probabilistic data association

the PDAF takes an expected value, which is the minimum mean square error (MMSE) estimate

- IPDAF : PDAF를 기반으로 트랙 존재 확률 개념을 추가 
- IMM-PDAF : 다중의 모델을 정의하고 각 모델의 가중치를 고려하여 상태를 추정 하는 IMM(Interacting Multiple Model)와 연계 


추적에 활용 방안 : 칼만필터의 갱신 단계에서 어떤 측정치를 사용하여 상태를 갱신 할지 결정하는 데이터 연관 기법은 IPDAF를 사용 



---

- the PDAF updates the track with a **weighted average** of all validated measurements

- The weights are the individual association probabilities






---

# [[추천] The Probabilistic Data Association Filter](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.212.383&rep=rep1&type=pdf)