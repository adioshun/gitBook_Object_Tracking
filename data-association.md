# Data Association

> 유사 표현?? Assignments Algorithm,  matching algorithm, Validation Gate (확인 필요)

정의 
    - 추적되고 있는 객체들에 올바른 관측치를 할당하는 것
    - assigning sensor responses to trajectories

데이터 연관 필터 
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) :



--- 

분류 방법 #1 

- 확률 기반: probabilistic data association [5], joint probabilistic data association [6], multiple hypothesis tracking [7] 
- 최적화 기반: Hungarian algorithm [16]
- 전역최적화 기반의 greedy 방법[17] 

분류 방법 #2
- Bayesian: compute a full (or approx.) distribution in DA space from priors, posterior beliefs, and observations
- Non-Bayesian: compute a maximum likelihood estimate from the possible set of DA solutions 

---
m-out-of-n기법 : n번 스캔에서 m번 연관된 정도를 살핌, 5회 미만 assign 실패시 Dead로 판단
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)


확률 기반 기법 : 연관필터에서 제공하는 존재 확률 기법 활용 
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) 기법


Assignment Problem = build a table of match scores

---


하나의 물체에 대해서 중복되어 발생하는 트랙을 조정하는 기법이다.

이는 두 개 또는 그 이상의 트랙이 실제 같은 물체를 추적하고 있는 경우에 하나의 트랙으로 만들어주는 역할을 한다. 
이를 트랙간 연관(TTTA : Track To Track Association)기법이라 한다. 트랙간 연관이 이루어진 후 트랙간 융합(TTTF : Track To Track Fusion) 기법을 통해 다중센서로부터 획득된 트랙들을 결합하여 하나의 트랙을 형성하게 되면 단일센서로부터 얻어진 값보다 추정오차가 개선된 추적이 가능하다.

이러한 중복된 트랙을 인지하고 삭제하기 위해 
- MHT(Multiple Hypothesis Tracking) 알고리듬에서는 N-scan back을 수행하여 같은 측정치를 연속적으로 사용하고 비슷한 상태 벡터를 사용하는 경우 트랙을 병합하여 트랙을 정확히 추정한다. 
- 그러나 대부분 사용하는 NNF, PDAF, JPDAF, IPDAF, LM-IPDAF등의 알고리듬은 No-scan back이다. 

---

## [Udacity](https://www.youtube.com/watch?v=DK1DIcPwCOU)





---

# [Robotics 2 Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf)

![](https://i.imgur.com/DGFjhYz.png)

- 데이터 수집 
- 측정값 예측 : 탐지 대상이 있을것 같은 **Area** 생성 
    - Area : Validation Gate라고 불리우며, 탐색 범위를 좁힐때 사용 됨   
- 측정값이 Area안에 있는지 확인 


#### 흐름 예시 : Multi-Target DA: Global NN 

1. Build the assignment matrix
2. Solve the linear assignment problem 
    - Hungarian method (blow up to square matrix)
    - Munkres algorithm for rectangular matrices
    - Finds global cost minimum! 
3. Check if assignments are in the validation gate
4. Performs DA jointly!


## Single Target Data Association

Non-Bayesian
- Nearest neighbor (NN)
    - Simple to implement
    - Can integrate wrong measurements (false alarms), and thus, produce overconfident estimates
    - Good if prediction and measurement models are accurate 

Bayesian
- Probabilistic Data Association Filter (PDAF)
    - A bit more involved to implement
    - Provide conservative estimates
    - Good in presence of high clutter and noisy models 
    

## Multi-Target Data Association 

Non Bayesian approaches
- Nearest neighbor
- Interpretation tree
- Joint compatibility (JCBB)

Bayesian approaches
- JPDAF
- MHT
- MCMC 






---

Youtube
- [Global Data Association for Multiple Pedestrian Tracking](https://www.youtube.com/watch?v=SgRSniLdpwk)
- [Object tracking](https://www.youtube.com/watch?v=liFAVoff9nM) : UCF CRCV 강좌 
- [Human Detection, Tracking and Segmentation in Surveillance Video](https://www.youtube.com/watch?v=f7PHLx3HoyQ&t=4s)


Slide
- Introduction to Data Association [[Part1]](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf), [[Part2]](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart2.pdf): ppt, CSE598C
- [Robotics 2Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf): 
- [People Tracking:Data Association](http://luthuli.cs.uiuc.edu/~daf/tutorials/activity/data_association.pdf): ppt


논문 
- [A Comparison of Data Association Techniques for Target Tracking in Clutter](https://pdfs.semanticscholar.org/c0d2/b5c5b6c8224688e47cd842db5693cc479548.pdf): 2002
- 적외선 영상에서 다수표적추적을 위한 LM-IHPDA 알고리듬 연구: 2013, 송택
- [3D-LIDAR Multi Object Tracking for Autonomous Driving](https://www.slideshare.net/adioshun/3dlidar-multi-object-tracking-for-autonomous-driving-111277160?qid=aa9596e3-5121-4eb1-bd53-89565da2c368&v=&b=&from_search=2): 석사 학위, 140p

코드 
- [Basic GNN Tracking](https://github.com/fbaeuerlein/BasicGNNTracking): C++

Ebook
- [handbook of multisensor data fusion](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVQnGoa2Foo-TjEF) :2001, CRC press
    - [Target Tracking Using Probabilistic Data Association-Based Techniques with Applications to Sonar,Radar, and EO Sensors](http://dsp-book.narod.ru/HMDF/2379ch08.pdf) : 8장 
- [Fundamentals of object tracking](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVVdlzNoLpMfexyk): 2011, 캠프리지 