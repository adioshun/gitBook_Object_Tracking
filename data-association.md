
데이터 연관 필터 
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) :











이러한 중복된 트랙을 인지하고 삭제하기 위해
MHT(Multiple Hypothesis Tracking) 알고리듬에서는
N-scan back을 수행하여 같은 측정치를 연속적으로 사
용하고 비슷한 상태 벡터를 사용하는 경우 트랙을 병
합하여 트랙을 정확히 추정한다. 그러나 대부분 사용
하는 NNF, PDAF, JPDAF, IPDAF, LM-IPDAF등의 알
고리듬은 No-scan back이며, 이 때

---

일반적으로 객체 추적을 위해서는 추적되고 있는 객체
들에 올바른 관측치를 할당하는 데이터연관(data association)
과정이 가장 중요하다[21]. 많이 알려진 확률 기반의 데이터
연관 방법으로는 probabilistic data association [5], joint
probabilistic data association [6], multiple hypothesis tracking [7] 등
이 있으며 최적화 기반의 데이터연관 방법으로는 Hungarian
algorithm [16], 전역최적화 기반의 greedy 방법[17] 등이 있다.



본 논문에서는 앞서 언급한 문제를 극복하고자 확률밀도
가정(Probability Hypothesis Density (PHD))필터를 이용하여 영
상기반의 온라인 다중객체추적을 구현한다. PHD 필터는 다
중 객체와 측정치들을 Random Finite Set에 근거하여 객체 집
합과 관측치 집합으로 모델링한다. 기존의 데이터연관 기반
의 추적 방식들과 다르게 PHD 필터는 각 객체를 독립적으
로 추정하기 보다 객체들을 하나의 집합으로 고려하여 추정
한다. 이러한 특징 때문에 각 객체에 하나의 관측지를 할당
하는 데이터연관 부분이 불필요하다. 또한, PHD 필터는 객체
의 사라짐, 출현, 그리고 검출 불확실성을 확률적으로 모델링
하여 표적 객체 관리와 검출 불확실성 관리를 필터링 과정에
서 자동적으로 처리할 수 있다는 장점이 있다.

---

[Global Data Association for Multiple Pedestrian Tracking](https://www.youtube.com/watch?v=SgRSniLdpwk): youtube 

[Object tracking](https://www.youtube.com/watch?v=liFAVoff9nM) : UCF CRCV 강좌 

Human Detection, Tracking and Segmentation in Surveillance Video : https://www.youtube.com/watch?v=f7PHLx3HoyQ&t=4s

[Introduction to Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf): ppt, CSE598C


[Robotics 2Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf): 


[People Tracking:Data Association](http://luthuli.cs.uiuc.edu/~daf/tutorials/activity/data_association.pdf): ppt


[A Comparison of Data Association Techniques for Target Tracking in Clutter](https://pdfs.semanticscholar.org/c0d2/b5c5b6c8224688e47cd842db5693cc479548.pdf): 2002

적외선 영상에서 다수표적추적을 위한 LM-IHPDA 알고리듬 연구: 2013, 송택

[3D-LIDAR Multi Object Tracking for Autonomous Driving](https://www.slideshare.net/adioshun/3dlidar-multi-object-tracking-for-autonomous-driving-111277160?qid=aa9596e3-5121-4eb1-bd53-89565da2c368&v=&b=&from_search=2): 석사 학위, 140p


[Basic GNN Tracking](https://github.com/fbaeuerlein/BasicGNNTracking): C++


[Ebook][handbook of multisensor data fusion](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVQnGoa2Foo-TjEF) :2001, CRC press
- 8장 : [Target Tracking Using Probabilistic Data Association-Based Techniques with Applications to Sonar,Radar, and EO Sensors](http://dsp-book.narod.ru/HMDF/2379ch08.pdf)

[eBook] [Fundamentals of object tracking](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVVdlzNoLpMfexyk): 2011, 캠프리지 