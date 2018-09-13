|논문명 |Confidence-Based Pedestrian Tracking in Unstructured Environments Using 3D Laser Distance Measurements |
| --- | --- |
| 저자\(소속\) | \(\) |
| 학회/년도 | 2014, [논문](https://userpages.uni-koblenz.de/~agas/Documents/Haeselich2014CBP.pdf) |
| Citation ID / 키워드 | Velodyne HDL-64E, SVM, 파티클 필터 |
| 데이터셋(센서)/모델 | |
| 관련연구|K. Kidono, Pedestrian recognition using high-definition LIDAR. In Proceedings, 2011|
| 참고 |  |
| 코드 |[ROS](https://github.com/koide3/hdl_people_tracking)|


# Confidence-Based Pedestrian Tracking

we address the problem of tracking multiple pedestrians in unstructured 3D point clouds by extracting and discarding additional candidates from vegetation and other structures. 


Our approach 
- works exclusively on LIDAR-based features and 
- uses split and merge steps that create additional candidates which are classified with a SVM

Tracking is performed by using a particle filter 
- where particles require a recurring re-detection with a high confidence value from the classifier. 
- Thus, we enforce a rapid disposal of particles without adequate re-activation.

## I. INTRODUCTION

차량 탐지 대비 보행자 탐지가 어려운 이유 `Pedestrians are challenging obstacles due to`
- the either stationary or moving state, 
- the highly varying appearance,
- and the complex movement characteristics. 
    - a pedestrian can move over difficult terrain surfaces and 
    - walk in arbitrary directions whereas cars are limited to the driving direction. 
- in groups, pedestrians might be walking very closely and occlude each other. 


본 논문에서는 
- In this work, the challenging task of accurately tracking pedestrians without tracking false positives over time is approached. 
- We describe an interaction-based approach between 
    - a detection algorithm using a Support Vector Machine (SVM) and 
    - a tracking algorithm based on particle filters. 
    

본 논문의 기여 `our own contribution consists of` 
- a new segmentation strategy using the dp-means algorithm [12] and
- the sophisticated interaction between the SVM confidence and the extinction of particles which is directly coupled to SVM re-detections in our approach. 

## II. RELATED WORK

Camera-based approaches ([6] for an overview) mostly address the problem by detecting and tracking pedestrians in single images or in video streams. 

```
[6] P. Dollar, C. Wojek, B. Schiele, and P. Perona. Pedestrian Detection: An Evaluation of the State of the Art. IEEE Transactions on Pattern Analysis and Machine Intelligence, 34(4):743–761, 2012.
```

In addition, several Laser-based approaches emerged over the past years using the data of 2D or 3D laser range finders (LRFs).


Breitenstein et al. [2] present a tracking-by-detection approach for multiple persons using particle filters in color image series. 
- Their implementation allows to track large numbers of moving pedestrians in 2D space without camera calibration or knowledge of the ground plane.

```
[2] M. Breitenstein, F. Reichlin, B. Leibe, E. Koller-Meier, and L. Gool. Robust Tracking-by-Detection using a Detector Confidence Particle Filter. In Proceedings of the IEEE International Conference on Computer Vision, pages 1515–1522, 2009
```

Petrovskaya and Thrun [16] present an approach to detect and track vehicle with a particle filter in 3D data. 
- Their generated model uses multiple rectangles for precise motion estimation of detected cars.

```
[16] A. Petrovskaya and S. Thrun. Model Based Vehicle Detection and Tracking for Autonomous Urban Driving. Autonomous Robots, Special Issue: Selected papers from Robotics: Science and Systems, 26(2–3):123–139, 2009.
```


Scholer et al. [19] use a Velodyne HDL-64E LRF to detect and track people in 3D point clouds. 
- Their approach allows to track partially and fully occluded persons over a certain amount of time in indoor areas.


```
[19] F. Scholer, J. Behley, V. Steinhage, D. Schulz, and A.B. Cremers. Person Tracking in Three-Dimensional Laser Range Data with Explicit Occlusion Adaption. In Proceedings of the IEEE International Conference on Robotics and Automation, pages 1297–1303, 2011.
```


Spinello et al. [21] present a combined bottom-up topdown detector for pedestrians in Velodyne HDL-64E data in
urban outdoor environments. 
- Their approach is independent from ground plane assumptions and the described detector uses a layered person model.
- For tracking, a multi-target multi-hypothesis approach is used and their system achieves high equal error rates within a limited range of 20 m.

```
[21] L. Spinello, M. Luber, and K. Arras. Tracking People in 3D Using a Bottom-Up Top-Down Detector. In Proceedings of the IEEE International Conference on Robotics and Automation, pages 1304–1310, 2011.
```

Navarro-Serment et al. [15] use geometric and motion features to detect and track pedestrians while driving in outdoor regions. 
- Their algorithm detects objects using a virtual 2D slice and then classifies each object using statistical pattern recognition techniques. 

```
[15] L. Navarro-Serment, C. Mertz, and M. Hebert. Pedestrian Detection and Tracking Using Three-dimensional LADAR Data. International Journal of Robotics Research, Special Issue: Seventh International Conference on Field and Service Robots, 29(12):1516–1528, 2010.
```



Kidono et al. [11] extend features of [15] by a slice feature and by reflection intensities of their Velodyne HDL-64E. 
- Their approach classifies pedestrians with a SVM in road environments and is able to deal with low spatial resolutions targets.


```
[11] K. Kidono, T. Miyasaka, A. Watanabe, T. Naito, and J. Miura. Pedestrian recognition using high-definition LIDAR. In Proceedings of the IEEE Intelligent Vehicles Symposium, pages 405–410, 2011.
```


Thornton et al. [23] present a multi-sensor approach including a 3D LRF for human detection and tracking in cluttered environments.


```
[23] S. Thornton, M. Hoffelder, and D. Morris. Multi-sensor Detection and Tracking of Humans for Safe Operations with Unmanned Ground Vehicles. In IEEE Workshop on Human Detection from Mobile Platforms, pages 103–112, 2008.
```

A probabilistic person detector on multiple layers of 2D laser range scans classified using AdaBoost [8] is presented by Mozos et al. [14]. 
- Each layer detects a different body part and the conducted experiments reveal robust detection rates in cluttered environments.

```
[14] O. Mozos, R. Kurazume, and T. Hasegawa. Multi-Part People Detection Using 2D Range Data. International Journal of Social Robotics, 2(1):31–40, 2010.
```


Premebida et al. [17] present a laser-based pedestrian detection system and focus on information extraction from LRFs. 
- In their work, the authors explore and describe the potential of LRFs in pedestrian classification and present results with different classification techniques using automotive and industrial LRFs


```
[17] C. Premebida, O. Ludwig, and U. Nunes. Exploiting LIDAR-based Features on Pedestrian Detection in Urban Scenarios. In Proceedings of the International IEEE Conference on Intelligent Transportation Systems, pages 405–410, 2009.
```

Carballo et al. [3] fuse multiple 2D LRFs on two layers to detect pedestrians in uncluttered indoor environments. 

```
[3] A. Carballo, A. Ohya, and S. Yuta. Fusion of Double Layered Multiple Laser Range Finders for People Detection from a Mobile Robot. In Proceedings of the IEEE International Conference on Multisensor Fusion and Integration for Intelligent Systems, pages 677–682, 2008.
```

Gidel et al. [9] present a pedestrian detection and tracking approach using an LRF system on multiple layers, too. 
- The proposed detector fuses the information from four layers and tracking is performed with a particle filter. 

```
[9] S. Gidel, P. Checchin, C. Blanc, T. Chateau, and L. Trassoudaine. Pedestrian Detection and Tracking in an Urban Environment Using a Multilayer Laser Scanner. IEEE Transactions on Intelligent Transportation Systems, 11(3):579–588, 2010.
```


Sato et al. [18] use an LRF with six scanning layers to track pedestrians with a Kalman filter in urban environments. 
- The approach maps objects with a certain height to a grid map and uses global nearest neighboring based data association.

```
[18] S. Sato, M. Hashimoto, M. Takita, K. Takagi, and T. Ogawa. Multilayer lidar-based pedestrian tracking in urban environments . In Intelligent Vehicles Symposium, pages 849–854, 2010.
```

## III. PEDESTRIAN DETECTION

### 3.1 Ground Removal

정의 : The Task of ground removal is to separate obstacle points from ground points (cf. [11], [15]) in order to reduce the computational load and to perform a first selection of candidates. 

```
[11] K. Kidono, T. Miyasaka, A. Watanabe, T. Naito, and J. Miura. Pedestrian recognition using high-definition LIDAR. In Proceedings of the IEEE Intelligent Vehicles Symposium, pages 405–410, 2011.
[15] L. Navarro-Serment, C. Mertz, and M. Hebert. Pedestrian Detection and Tracking Using Three-dimensional LADAR Data. International Journal of Robotics Research, Special Issue: Seventh International Conference on Field and Service Robots, 29(12):1516–1528, 2010.
```

높이 정보를 기준으로 하면 실패 가능성이 높다. `In unstructured environments, an assumption of a planar ground surface with a fixed ground height is likely to fail. `
- Planar ground regions are often interrupted by hills, ditches, and other surface variations. 

In our approach, 
1. we first insert the 3D data into a three-dimensional grid with a resolution of $$0.1 × 0.1 × 0.1m^3$$ per cell. 
2. Afterwards, the cells are sorted according to their height(computed from the highest and the lowest point in each cell) from high to low. 
3. Each of those candidate cell is not only classified wrt. the contained points, but also wrt. the neighboring cells. 
4. A sliding window with a height threshold is used to calculate the absolute difference between the highest and the lowest point among all point of the current cell and in addition all points of neighboring cell. 
5. Based on the resulting values, a cell is classified as Empty, Ground or Obstacle

### 3.2 Clustering

The ground removal algorithm yields groups of cells which contain obstacles. 

Afterwards, those groups need to be prepared for **feature extraction** and **classification**. 

- On the one hand, the clustering algorithm needs to cluster obstacle cells to groups of sufficiently large 3D distance measurements which represent pedestrian candidates. 

- On the other hand, the algorithm needs to split up large groups of 3D points in order to separate pedestrians from other obstacles which are close to them, including trees, building and other pedestrians.

Our approach consists of two steps and aims to find a high number of pedestrian candidates even if they are located close to other objects. 

We explicitly choose not to discard anything in the slightest similarity to a human. 

Thus, our next step is to further analyze clusters that are too large to represent a single candidate, which in turn yields increased runtime. 

In order to keep the overall runtime low, several algorithms were inspected. 

- k-mean 방법은 k값과, 초기설정이 필요한 단점이 있다. `Approaches like k-means [13] exhibit fast runtimes but the original algorithm requires`
    - knowledge of the number of clusters k in advance and 
    - an imprecise initial configuration of the medians may drastically increase the runtime. 

- 해결책 #1 : The k-means++ extension [1] improves the initial distribution and provides faster runtimes. 

- 해결책 # 2 : The problem of an unknown k is solved by the dp-means algorithm [12], which we use and that starts with k = 1 and increments it, if a cluster grows too large, and in addition exhibits fast runtimes. 

```
[1] D. Arthur and S. Vassilvitskii. K-means++: The Advantages of Careful Seeding. In Proceedings of the Annual ACM-SIAM Symposium on Discrete Algorithms, pages 1027–1035, 2007
[12] B. Kulis and M. Jordan. Revisiting k-means: New Algorithms via Bayesian Nonparametrics. In Proceedings of the International Conference on Machine Learning, pages 513–520, 2012.
```

A resulting separated cluster is exemplary shown in Fig. 1 where the replaced cluster is framed in blue and the
new clusters are framed in green.

![](https://i.imgur.com/mmsurMa.png)

The aforementioned step results in an over-clustering of large obstacles, which are now separated wrt. the extent of pedestrians. 

Hence, our next step is to re-merge nearby clusters without a gap between them. 

The distance between the centers of two clusters is divided into eight histogram bins and if the two bins in the middle contain less than 80% of the measurements compared to the average number of measurements in all bins, a gap is detected. 

![](https://i.imgur.com/H0kaInu.png)

An example of re-merged clusters is shown in Fig. 2. Here, the new smaller clusters cannot be separated adequately and the original group is maintained. 

This strategy has the advantage of finding pedestrian candidates close to any other obstacles at the expense of an increased runtime and the possibility of more false-positives.



### 3.3 Features (7개)

Our feature vector per cluster consists of 8 different features introduced in the literature, 
- where f1 and f2 are presented by Premebida et al. [17] and describe the number of points included in a cluster and the minimum distance of the cluster to the sensor. 
- Navarro-Serment et al. [15] apply a Principal Component Analysis (PCA) to the clusters, which represents f3 to f7. 

Those features are the 3D covariance matrix of a cluster, the normalized moment of inertia tensor, the 2D covariance matrix in different zones (cf. [15]), the normalized 2D histogram for the main plane and the normalized 2D histogram for the secondary plane. 

In another approach, Kidono et al. [11] introduce two additional features. 
- The first one, the slice feature of a cluster, forms our last feature f8 and aims to differentiate pedestrians from false positives in the shape of trees or poles. 
    - A cluster is partitioned into slices along the z-axis and for each slice the first and second largest eigenvalue is calculated. 
    - As the descriptive power of the slice feature decreases over longer distances, only a rough estimate remains in long distances.
- The other feature introduced by Kidono et al. considers the distribution of the reflection intensities in the cluster. 
    -Since our LRF is not calibrated wrt. the intensities, this feature could not be integrated.

```
[17] C. Premebida, O. Ludwig, and U. Nunes. Exploiting LIDAR-based Features on Pedestrian Detection in Urban Scenarios. In Proceedings of the International IEEE Conference on Intelligent Transportation Systems, pages 405–410, 2009
[15] L. Navarro-Serment, C. Mertz, and M. Hebert. Pedestrian Detection and Tracking Using Three-dimensional LADAR Data. International Journal of Robotics Research, Special Issue: Seventh International Conference on Field and Service Robots, 29(12):1516–1528, 2010
[11] K. Kidono, T. Miyasaka, A. Watanabe, T. Naito, and J. Miura. Pedestrian recognition using high-definition LIDAR. In Proceedings of the IEEE Intelligent Vehicles Symposium, pages 405–410, 2011.    
```    
        
                
### 3.4 Classification & Training

분류 목적 : 이진 분류 (사람 or NOT) `The task of the classifier is to perform a binary classification
between pedestrian and non-pedestrian as precise as possible.`

알고리즘 :SVM + RBF 커널 `As proposed by Kidono et al. [11], we use a SVM with radial basis function (RBF) Kernel [4], [5] together`

```
[11] K. Kidono, T. Miyasaka, A. Watanabe, T. Naito, and J. Miura. Pedestrian recognition using high-definition LIDAR. In Proceedings
[4] C.-C. Chang and C.-J. Lin. LIBSVM: A library for Support Vector Machines. ACM Transactions on Intelligent Systems and Technology, 2(3):27:1–27:27, 2011.
[5] C. Cortes and V. Vapnick. Support-Vector Networks. Machine Learning, 20(3):273–297, 1995.
```

Feature : 본 논문 3.3에서 언급한 특징들

학습 데이터 : For training the SVM we annotated pedestrians in different datasets from the campus Koblenz of the University of Koblenz-Landau, 
- which contain vegetation, trees and buildings.
- Positive samples are extracted from annotations and negative samples are generated at random from clusters that have not been marked as pedestrians by a human annotator.

학습 알고리즘 : For this work, we used the LIBSVM library from Chang and Lin [4] that computes a separating hyperplane which
discriminates between the pedestrian and non-pedestrian.

```
[4] C.-C. Chang and C.-J. Lin. LIBSVM: A library for Support Vector Machines. ACM Transactions on Intelligent Systems and Technology, 2(3):27:1–27:27, 2011.
```

분류 이후 작업 : Our classifier returns a vector of confidence values in [0, 1] for each class how likely a candidate belongs to the class. 
- The probability of the highest rated class is used as input value for the tracking system

## IV. PEDESTRIAN TRACKING

Our initial idea for the tracking was to use virtual 2D scans and was inspired by Petrovskaya and Thrun [16]. 

With an adopted measurement model we observed that, with a high resolution 2D scan, many pedestrians could be successfully tracked. 

Unlike, in urban scenarios varying inclination angles of the terrain and many occlusions, e.g. caused by vegetation, are problematic. 

Hence, we developed a new measurement model and decided to focus on an sophisticated interaction of the detection algorithm with the particle filter. 

This allows our approach to discard hypotheses early and enables it to deal efficiently with false detection that occur frequently in unstructured environments.



### 4.1 Measurement Model

### 4.2 Particle Filter & Particle Extinction

## V. EXPERIMENTS

## VI. DISCUSSIONS

## VII. CONCLUSIONS

We presented an approach for pedestrian tracking in unstructured environments that aims to identify pedestrians
close to vegetation by using split and merge strategies on 3D clusters. 

While the algorithms separate pedestrians from other structures, a great number of newly created candidates
affect precision and runtime. 

The proposed tracking approach performs well in all test environments, especially when regarding the low recall values of the SVM in cluttered environments. 

The SVM is unable to deal with a divergent update frequency of the Velodyne HDL-64E, thus lowering precision and recall on the publicly available datasets and creating a further challenge for the tracking system which proved reliable under these complicated circumstances.




