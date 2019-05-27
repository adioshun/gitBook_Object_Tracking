PDA 
- 유효게이트에 들어 오는 모든 측정치를 이용하여 항적을 유지 



NN
- 각 항적에 대한 특정의 예측치에 가장 가까운 측정치를 그 항적에 연계시켜 항적을 유지해 나감 


prediction: propagate state pdf forward in time,taking process noise into account (translate, deform,and spread the pdf)

Data association to determine best match

update: use Bayes theorem to modify prediction pdf based on current measuremen

---

[Data Association](http://luthuli.cs.uiuc.edu/~daf/tutorials/activity/Trackingbasicsblock.pdf)
- Nearest neighbours
    - choose the measurement with highest probability given predicted state
    - popular, but can lead to catastrophe
- Probabilistic Data Association
    - combine measurements, weighting by probability given predicted state
    - gate using predicted state