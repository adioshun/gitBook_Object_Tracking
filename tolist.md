CAMshift 기법과 칼만 필터를 결합한 객체 추적 시스템, 2013




[Object (e.g Pedestrian, vehicles) tracking by Extended Kalman Filter (EKF), with fused data from both lidar and radar sensors.](https://github.com/JunshengFu/tracking-with-Extended-Kalman-Filter)



---
- ~~[Object Detection and Tracking with Side Cameras and RADAR in an Automotive Context](http://www.mi.fu-berlin.de/inf/groups/ag-ki/Theses/Completed-theses/Master_Diploma-theses/2013/Hofmann/Master-Hofmann.pdf?1381479774)~~: 2013, 3장이 센서 퓨전

- ~~[Survey on Object Detection and Tracking Using Fusion Approach](https://www.ijircce.com/upload/2016/march/98_24_Survey.pdf)~~: 2016, 8P, 일반적 설명

- [Particle Filter Implementation](https://medium.com/@andrew.d.wilkie/self-driving-car-engineer-diary-9-898f075e888c): 하단

- 추천 : [Tracking pedestrians for self driving cars](https://medium.com/towards-data-science/tracking-pedestrians-for-self-driving-cars-ccf588acd170)
- 추천 : [Tracking a self-driving car with high precision](https://medium.com/@priya.dwivedi/latest)





## 1. List

- 깃북 : [칼만필터](https://adioshun.gitbooks.io/deep_drive/content/introfusion.html)

## 2. Paper

- [LiDAR Based Real Time Multiple Vehicle Detection and Tracking](https://waset.org/publications/10004678/lidar-based-real-time-multiple-vehicle-detection-and-tracking): 3.D Data Association and Tracking

- ~~A New Upsampling Method for Mobile LiDAR Data~~, Ruisheng Wang, Jeff Bach, Jane Macfarlane, NAVTEQ Corporation
    - 카메라 + Lidar연계, upsample mobile LiDAR data using panoramic images


- Upsampling Range Data in Dynamic Environments, Jennifer Dolson
    - 카메라 + Lidar 연계


- LidarBoost: Depth Superresolution for ToF 3D Shape Scanning, Sebastian Schuon(스탠포드)
    - 스트레오 카메라활용 combines several low resolution noisy depth images of a static scene from slightly displaced viewpoints, and merges them into a high-resolution depth image


- [Semantically Guided Depth Upsampling](https://arxiv.org/abs/1608.00753), Nick Schneider, 2016
    - 이지미 정보 활용, Lidar 업샘플링 기법 upsampling of sparse depth(Lidar) data, guided by high-resolution **imagery**.


- DenseLidarNet : 카메라 + Lidar, [[깃허브]](https://github.com/345ishaan/DenseLidarNet)

- [Extended Object Tracking: Introduction, Overview and Applications](https://arxiv.org/abs/1604.00970): arXiv2017

- [3D-LIDAR Multi Object Tracking for Autonomous Driving](https://repository.tudelft.nl/islandora/object/uuid%3Af536b829-42ae-41d5-968d-13bbaa4ec736): 석사 학위 2017

- [Robust Real-Time Tracking Combining 3D Shape, Color, and Motion](http://davheld.github.io/DavidHeld_files/ijrr_tracking.pdf): 2015, 28page

- [Simultaneous Localization, Mapping and Moving Object Tracking](https://pdfs.semanticscholar.org/1c8e/ab35f14011e8394a6f92c7fad1b4cedd764d.pdf): 박사 학위 2004 [47p](http://repository.cmu.edu/cgi/viewcontent.cgi?article=1062&context=robotics)


- [Track, then Decide: Category-Agnostic Vision-based Multi-Object Tracking](https://www.vision.rwth-aachen.de/publication/00162/) : ICRA2018


## 3. Article (Post, blog, etc.)



## 3. Tutorial (Series, )



## 4. Youtube
- [Vehicle Detection using LiDAR and Camera sensor Fusion](https://www.youtube.com/watch?v=V3cN5LrPr4M)

- [Why You Should Use The Kalman Filter Tutorial - Pokemon Example](https://www.youtube.com/watch?v=bm3cwEP2nUo)

- Very simple example of Multi object tracking using the Kalman filter and then Hungarian algorithm. : Student Dave
    - [YOUTUBE](https://www.youtube.com/watch?v=Me0wbxEDO4I) : 1~4
    - [Homepage](http://studentdavestutorials.weebly.com/)


## 6. Material (Pdf, ppt)



## 7. Implementation (Project)

- [3차원 포인트 클라우드 스캔 기반 객체 추적](http://daddynkidsmakers.blogspot.com/2015/08/3_29.html): ROS 적용


- [Object Tracking with Sensor Fusion-based Extended Kalman Filter](https://github.com/JunshengFu/tracking-with-Extended-Kalman-Filter)

- [An extended Kalman Filter implementation in Python for fusing lidar and radar sensor measurements](https://github.com/mithi/fusion-ekf-python): 파이썬, 라이다+레이다.


- [추천] [Multi Object Tracker Using Kalman Filter & Hungarian Algorithm](https://github.com/srianant/kalman_filter_multi_object_tracking): 2D, python, 2017

- [Object-Tracking-and-Detection](https://github.com/infparadox/Object-Tracking-and-Detection): python



- ~~[Object Tracking using OpenCV (C++/Python)](https://www.learnopencv.com/object-tracking-using-opencv-cpp-python/)~~ : OpenCV지원 알고리즘을 이용한 간단한 구현(point 예측)
  - OpenCV : [Motion Analysis and Object Tracking](https://docs.opencv.org/2.4/modules/video/doc/motion_analysis_and_object_tracking.html?highlight=kalman%20filter#cv2.KalmanFilterhttp://), [kalman.py](https://github.com/opencv/opencv/blob/master/samples/python/kalman.py)


- [KITTI Track Collection (KTC) devkit](https://github.com/aljosaosep/kitti-track-collection)


## 8. Research Group / Conference

- [KITTI Object Tracking Evaluation 2012](http://www.cvlibs.net/datasets/kitti/eval_tracking.php)
    - [This file describes the KITTI tracking benchmarks](https://github.com/pratikac/kitti/blob/master/readme.tracking.txt)


---
---
