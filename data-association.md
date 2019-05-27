# Data Association

정의 
    - 추적되고 있는 객체들에 올바른 관측치를 할당하는 것
    - assigning sensor responses to trajectories

데이터 연관 필터 
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) :


분류 방법 #1 

- 확률 기반: probabilistic data association [5], joint probabilistic data association [6], multiple hypothesis tracking [7] 
- 최적화 기반: Hungarian algorithm [16]
- 전역최적화 기반의 greedy 방법[17] 

분류 방법 #2
- Bayesian: compute a full (or approx.) distribution in DA space from priors, posterior beliefs, and observations
- Non-Bayesian: compute a maximum likelihood estimate from the possible set of DA solutions 





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