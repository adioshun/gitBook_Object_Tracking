Youtube
- [Global Data Association for Multiple Pedestrian Tracking](https://www.youtube.com/watch?v=SgRSniLdpwk)
 - GMCP Tracker
 - GMMCP Tracker
 - Crowd Tracker 
- [Object tracking](https://www.youtube.com/watch?v=liFAVoff9nM) : UCF CRCV 강좌
- [Human Detection, Tracking and Segmentation in Surveillance Video](https://www.youtube.com/watch?v=f7PHLx3HoyQ&t=4s)


Slide
- Introduction to Data Association [[Part1]](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf), [[Part2]](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart2.pdf): ppt, CSE598C
- [[추천] Robotics 2Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf):
- [People Tracking:Data Association](http://luthuli.cs.uiuc.edu/~daf/tutorials/activity/data_association.pdf): ppt
- [[추천] Human-Oriented Robotics-Tracking and Data Association](http://srl.informatik.uni-freiburg.de/teachingdir/ws13/slides/11-TemporalReasoning-3.pdf)

논문
- [A Comparison of Data Association Techniques for Target Tracking in Clutter](https://pdfs.semanticscholar.org/c0d2/b5c5b6c8224688e47cd842db5693cc479548.pdf): 2002
- 적외선 영상에서 다수표적추적을 위한 LM-IHPDA 알고리듬 연구: 2013, 송택
- [3D-LIDAR Multi Object Tracking for Autonomous Driving](https://www.slideshare.net/adioshun/3dlidar-multi-object-tracking-for-autonomous-driving-111277160?qid=aa9596e3-5121-4eb1-bd53-89565da2c368&v=&b=&from_search=2): 석사 학위, 140p

코드
- [Basic GNN Tracking](https://github.com/fbaeuerlein/BasicGNNTracking): C++
- [A Python utility package for multiple object tracking](https://github.com/nwojke/pymotutils): python
- [JPDAFTracker](https://github.com/apennisi/jpdaf_tracking): c++
- [Graph Neural Based End-to-end Data Association Framework for Online Multiple-Object Tracking](https://github.com/peizhaoli05/EDA_GNN)
- [trackpy](https://github.com/soft-matter/trackpy):  a Python package for particle tracking in 2D, 3D
- [IOU Tracker](https://github.com/bochinski/iou-tracker) : python 
- [Multiple Target Filtering Library](https://github.com/nathanlem1/MTF-Lib) : python 
- [[추천]TrackerComponentLibrary](https://github.com/USNavalResearchLaboratory/TrackerComponentLibrary) : matlab 다양한 추적 알고리즘 구현 
 - [Basic Tracking Examples-JPDAF and nearest neighbor filters](https://github.com/USNavalResearchLaboratory/TrackerComponentLibrary/blob/master/Sample%20Code/Basic%20Tracking%20Examples/demo2DDataAssociation.m)
 - [0) GNN-JPDA, 1) JPDA 2) GNN 3) Parallel single-target PDAs 4) Naïve nearest neighbor 5) JPDA* 6) Approximate GNN-JPDA 7) Approximate JPDA  8) Set JPDA 9) Naïve nearest neighbor JPDA 10) Approximate naïve nearest neighbor JPDA ](https://github.com/USNavalResearchLaboratory/TrackerComponentLibrary/blob/master/Assignment%20Algorithms/singleScanUpdate.m) : matlab
- multiple hypotheses tracking (MHT): [matlab ](http://rehg.org/mht/), [c++](https://ingemarcox.cs.ucl.ac.uk/?page_id=9)
- [Single Target with RFS Observations Filter, Bernoulli Filter, PHD Filter, CPHD Filter, Cardinality Balanced Multi-Bernoulli Filter, Robust PHD/CPHD/MB Filters, Generalized Labeled Multi-Bernoulli Filter (separate plus joint recursion implementations), Labeled Multi-Bernoulli Filter (separate plus joint recursion implementations), OSPA Metric OSPA(2) Metric](http://ba-tuong.vo-au.com/codes.html): matlab
- [BayesTracking - a library for Bayesian tracking](https://github.com/lcas/bayestracking): C++, ROS, 3D, LCAS

Ebook
- [handbook of multisensor data fusion](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVQnGoa2Foo-TjEF) :2001, CRC press
- [Target Tracking Using Probabilistic Data Association-Based Techniques with Applications to Sonar,Radar, and EO Sensors](http://dsp-book.narod.ru/HMDF/2379ch08.pdf) : 8장
- [Fundamentals of object tracking](https://1drv.ms/b/s!Ag9W8Hm9qZzrzVVdlzNoLpMfexyk): 2011, 캠프리지

---
# 추천 자료 

하지만 트래킹에 대한 전반적인 이해를 돕기 위해서 책을 하나 추천 드리면



```
Yaakov Barshalom, X. Rong Li, Estimation with Applications to Tracking and Navigation
```
https://onlinelibrary.wiley.com/doi/book/10.1002/0471221279
http://read.pudn.com/downloads117/ebook/497286/Estimation%20with%20Applications%20to%20Tracking%20and%20Navigation%E6%9D%8E%E6%99%93%E6%A6%95.pdf

입니다. 저는 처음이 책을 접하지 않고 두서없이 공부를 하였지만 제가 추천 드리는 책이 제가 생각하기로는 기본적인 트래킹 알고리즘에 대한 설명이 잘 되어 있는 것으로 생각됩니다. 




그 다음으로는 비선형 시스템의 상태를 추적할 경우 필요한 extended kalman filter, unscented kalman filter, particle filter에 대해 연구하시고 싶으시면 아래 논문과 책을 보시면 도움이 되실거라 생각됩니다.


```
S.J. Julier, and J.K. Uhlmann, “New Extension of the Kalman Filter to Nonlinear Systems,” Proceedings of the SPIE 3068, Signal Processing, Sensor Fusion, and Target Recognition VI, pp. 182-193,1997.
 S.J. Julier, and J.K. Uhlmann, “Unscented Filtering and Nonlinear Estimation,” Proceedings of the IEEE, vol. 92, no. 2, pp. 401-422, 2004.
B. Ristic, S. Arulampalam, N. Gordon, Beyond the Kalman Filter. Artech House:Norwood, MA, USA, 2004.
```



다음으로 data association에 대해 연구하시려면 아래 책과 기본적인 NN, SN, PDA를 위한 논문을 읽어 보시면 많은 도움이 되리라 생각됩니다.

```
Y. Bar-Shalom and T. E. Fortmann, Tracking and data association. New York:Academic, 1988.
X.R. Li, and Y. Bar-Shalom, “Tracking in Clutter with Nearest Neighbor Filters: Analysis and Performance,” IEEE Transactions on Aerospace and Electronic Systems, vol. 32, no. 3, pp. 995-1010, 1996.
X.R. Li, “Tracking in Clutter with Strongest Neighbor Measurements - Part I: Theoretical Analysis,” IEEE Transactions on Automatic Control, vol. 43, no. 11, pp. 1560-1578, 1998.
Y. Bar-Shalom, and E. Tse, “Tracking in a Cluttered Environment with Probabilistic Data Association,” Automatica, pp. 451-460, Sep. 1975.
```


특히 Y. Bar-Shalom이 지은 책 두권은 표적 추적에 관련하여 매우 좋은 책으로 생각됩니다. 최대한 간추리고 기본적인 알고리즘들에 대한 논문과 책을 소개 시켜 드립니다. 소개드린 논문과 책 말고 좀더 심도 있는 연구가 필요하시면 (예를 들어 track management, multi-target tracking algorithm 등)에 관심이 있으시면 연락 주시면 관련 자료들을소개 시켜 드리겠습니다. 

---

# [CVPR 2019 Tracking](https://github.com/shijieS/ComputerVisionSummarization#7-tracking)

- [Multivariate Kalman Filters - Working with Multiple State Variables](https://github.com/shijieS/ComputerVisionSummarization/blob/master/codebook/06-Multivariate-Kalman-Filters.ipynb): 쥬피터



