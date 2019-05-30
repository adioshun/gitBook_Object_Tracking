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
    
    
---

# [Tracking and Data Association](http://srl.informatik.uni-freiburg.de/teachingdir/ws13/slides/11-TemporalReasoning-3.pdf)

- Detection is knowing the presence of an object, possibly with some attribute information

- Tracking is estimating the state of a moving object over time based on remote measurements

- Tracking also involves maintaining the identity of an object over time despite detection errors (FN, FP) and the presence of other objects

- Tracking may involve estimating the state of several objects at a time. This gives rise to origin uncertainty, that is, uncertainty about which object generated which observation

- Data association addresses the origin uncertainty problem. It’s the process of associating uncertain measurements to known tracks

- Data association may involve interpreting measurements as new tracks, false alarms or misdetections and tracks as occluded or terminated

