|논문명 |Online learning for human classification in 3D LiDAR-based tracking |
| --- | --- |
| 저자\(소속\) | \(\) |
| 학회/년도 | 2017, [논문](http://webpages.lincoln.ac.uk/nbellotto/doc/Yan2017.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | [홈페이지](http://lcas.lincoln.ac.uk/wp/), [저자](https://yzrobot.github.io/), [Youtube](https://www.youtube.com/watch?v=bjztHV9rC-0) |
| 코드 ||


연구 History

|년도|1st 저자|논문명|코드|
|-|-|-|-|
|2007|Nicola Bellotto|[PEOPLE TRACKING WITH A MOBILE ROBOT: A COMPARISON OF KALMAN AND PARTICLE FILTERS](http://www.robots.ox.ac.uk/~nick/doc/Bellotto2007b.pdf)||
|2010|Nicola Bellotto|[Computationally Efficient Solutions for Tracking People with a Mobile Robot: an Experimental Evaluation of Bayesian Filters](http://webpages.lincoln.ac.uk/nbellotto/doc/Bellotto2010.pdf)||
|2017|Zhi Yan|[Online learning for human classification in 3D LiDAR-based tracking](http://webpages.lincoln.ac.uk/nbellotto/doc/Yan2017.pdf)|[github](https://github.com/yzrobot/online_learning) |
|2018|Zhi Yan|[Multisensor Online Transfer Learning for 3D LiDAR-based Human Detection with a Mobile Robot](https://arxiv.org/pdf/1801.04137.pdf)|[Github](https://github.com/LCAS/online_learning/tree/multisensor)|



## 2. RELATED WORK

휴먼 탐지/트래킹 관련 연구 `Human detection and tracking have been widely studied in recent years.`

- 대부분의 연구는 **RGB-D 카메라** 를 이용하였으며, 제약적인 탐지 범위와 FoV를 가지고 있다. `Many popular approaches are based on RGB-D cameras [12], [13], although these have limited range and field of view. `

- Lidar가 대안이 될수 있지만, 포인트클라우드의 적은 정보로 사람을 인지 하는 것이다. `3D LiDARs can be an alternative, but one of the main challenges working with these sensors is the difficulty of recognizing humans using only the relatively low information they provide. `


### 2.1 그룹화

- 가능한 접근법은 그룹화 하는것이다. `A possible approach to detect humans is by clustering point clouds in depth images or 3D laser scans. `

- For example,
  - Rusu [14] presented a straightforward but computationally expensive method based on Euclidean distance.
  - Bogoslavskyi and Stachniss [15] proposed a faster approach, although the computational efficiency limits the clustering precision.

```
[14] R. B. Rusu, “Semantic 3D object maps for everyday manipulation in human living environments,” Ph.D. dissertation, Computer Science department, Technische Universitaet Muenchen, Germany, 2009.
[15] I. Bogoslavskyi and C. Stachniss, “Fast range image-based segmentation of sparse 3d laser scans for online operation,” in Proceedings of the 2016 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), 2016, pp. 163–169.
```

### 2.2 분류기 학습 (Offline)

-일반적인 접근법은 분류기를 학습시켜 사용하는 것이다. `A very common approach is to use an offline trained classifier for human detection. `


- For example,
  - 7개의 특징값을 SVM을 이용하여 학습 `Navarro-Serment et.al. [1], introduced seven features for human classification and trained an SVM classifier based on these features. `
  - 2개의 특징값을 추가 `Kidono et al. [3] proposed two additional features considering the 3D human shape and the clothing material (i.e. using the reflected laser beam intensities), showing significant classification improvements. ``
  - 샘플링방식으로 향상 `Li et al. [7] implemented instead a resampling algorithm in order to improve the quality of the geometric features proposed by the former authors.`
  - 탑다운 분류기 & 다운업 탐지기 사용 `Spinello et al. [4] combined a top-down classifier based on volumetric features and a bottom-up detector, to reduce false positives for distant persons tracked in 3D LiDAR scans.`
  - 슬라이딩 윈도우 이용 `Wang and Posner [8] applied a sliding window approach to 3D point data for object detection, including humans.`
    - They divided the space enclosed by a 3D bounding box into sparse feature grids,
    - then trained a linear SVM classifier based on six features related to the occupancy of the cells,
    - the distribution of points within them, and the reflectance of these points.

```
[1] L. E. Navarro-Serment, C. Mertz, and M. Hebert, “Pedestrian detection and tracking using three-dimensional ladar data,” in Proceedings of the 7th Conference on Field and Service Robotics (FSR), 2009, pp. 103–112.
[3] K. Kidono, T. Miyasaka, A. Watanabe, T. Naito, and J. Miura, “Pedestrian recognition using high-definition LIDAR,” in Proceedings of the 2011 IEEE Intelligent Vehicles Symposium (IV), 2011, pp. 405–410.
[7] K. Li, X. Wang, Y. Xu, and J. Wang, “Density enhancement-based long-range pedestrian detection using 3-d range data,” IEEE Transactions on Intelligent Transportation Systems, vol. 17, pp. 1368–1380, 2016.
[4] L. Spinello, M. Luber, and K. O. Arras, “Tracking people in 3d using a bottom-up top-down detector,” in Proceedings of the 2011 IEEE International Conference on Robotics and Automation (ICRA), 2011, pp. 1304–1310.
[8] D. Z. Wang and I. Posner, “Voting for voting in online point cloud object detection,” in Proceedings of Robotics: Science and Systems, 2015.
```

- 학습기반 방식의 제약 : The problem with offline methods, though, is that the classifier needs to be manually retrained every time for new environments.


### 2.3 Tracking

- 위 방법들은 Lidar데이터에서 학습된 분류기를 통해서 사람을 탐지 하는 방법 들이다. `The above solutions rely on pre-trained classifiers to detect humans from the most recent LiDAR scan. `

- tracking을 통해서 사람 탐지 하는것은 많이 연구 되진 않았다. `Only a few methods have been proposed that use tracking to boost human detection. `

- for example,
  - 확장 칼만필터를 이용하여 탐지력 높임 `Shackleton et al. [2],  employed an Extended Kalman Filter to estimate the position of a target and assist human detection in the next LiDAR scan. `
  - 준-지도 학습 방법을 이용 `Teichman et al. [5] presented a semi-supervised learning method for track classification. `
    - Their method requires a large set of labeled background objects (i.e. no pedestrians) to trains classifiers offline,
    - which showed good performances for track classification but not for object recognition.

```
[2] J. Shackleton, B. V. Voorst, and J. A. Hesch, “Tracking people with a 360-degree lidar,” in Proceedings of the Seventh IEEE International Conference on Advanced Video and Signal Based Surveillance (AVSS), 2010, pp. 420–426.
[5] A. Teichman and S. Thrun, “Tracking-based semi-supervised learning,” International Journal of Robotics Research (IJRR), vol. 31, no. 7, pp. 804–818, 2012.
```

### 2.4 annotation-free methods

-깊이 카메라와 다르게 데이터 셋이 별로 없다. `Besides datasets collected with RGB-D cameras [12], [13],[16], there are a few 3D LiDAR datasets available to the scientific community for outdoor scenarios [4], [6], [9], [17], but not with annotated data for human tracking in large indoor environments, like the one presented here.`


- Some authors proposed annotation-free methods.
  - 비지도 학습 방식 3D--> 2D 투영 `Deuge et al. [6] introduced an unsupervised feature learning approach for outdoor object classification by projecting 3D LiDAR scans into 2D depth images. `
  - 움직임 정보를 기반으로 `Dewan et al. [18] proposed a model-free approach for detecting and tracking dynamic objects, which relies only on motion cues. `

```
[6] M. D. Deuge, A. Quadros, C. Hung, and B. Douillard, “Unsupervised feature learning for classification of outdoor 3d scans,” in Proceedings of the Australasian Conference on Robotics and Automation (ACRA), 2013.
[18] A. Dewan, T. Caselitz, G. D. Tipaldi, and W. Burgard, “Motion-based detection and tracking in 3D LiDAR scans,” in Proceedings of the 2016 IEEE International Conference on Robotics and Automation (ICRA), 2016, pp. 4508–4513.
```


- 하지만 이 방법들은 별로 좋지 않다 `These methods, however, are either not very accurate or unsuitable for slow and static pedestrians.`
