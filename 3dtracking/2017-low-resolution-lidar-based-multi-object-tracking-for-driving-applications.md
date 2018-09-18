|논문명 |Low resolution lidar-based multi-object tracking for driving application |
| --- | --- |
| 저자\(소속\) | \(\) |
| 학회/년도 | 2017, [논문](http://www.iri.upc.edu/files/scidoc/1924-Low-resolution-lidar-based-multi-object-tracking-for-driving-applications.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | -|
| 코드 | -|




# Low resolution lidar-based multi-object tracking for driving applications


# Abstract

we developed a lidar-based system that uses a Convolutional Neural Network (CNN), to perform pointwise vehicle detection using PUCK data, and Multi-Hypothesis Extended Kalman Filters (MH-EKF), to estimate the actual position and velocities of the detected vehicles.

# 1.  Introduction

- 기존 Geometrical 접근 법 `Lidar point clouds have been traditionally processed following geometrical approaches like in [20].`

  ```
  20. Petrovskaya, A., Thrun, S.: Model based vehicle detection and tracking for autonomous urban driving. Autonomous Robots 26(2-3), 123–139 (2009)  
  ```

- 최근 딥러닝 방식으로 좋은 성과 보임 `However, recent works [8], [5] are pointing at Deep Learning techniques as powerful tools to extract information from point clouds, expanding their applicability beyond image processing tasks. `

  ```
  8. Engelcke, M., Rao, D., Wang, D.Z., Tong, C.H., Posner, I.: Vote3deep: Fast object detection in 3d point clouds using efficient convolutional neural networks. In: Robotics and Autom. (ICRA), 2017 IEEE Int. Conf. on, pp. 1355–1361. IEEE (2017)
  5. Chen, X., Ma, H., Wan, J., Li, B., Xia, T.: Multi-view 3d object detection network for autonomous driving. arXiv preprint arXiv:1611.07759 (2016)
  ```

- 저자는 HDL-64로도 비슷한 연구를 진행 하였음 `In previous works [26], we developed a vehicle lidar-based tracking system that used a Fully Convolutional Network (FCN) to perform per-point data segmentation using a Velodyne HDL64 sensor. `

  ```
  26. Vaquero, V., del Pino, I., Moreno-Noguer, F., Sol`a, J., Sanfeliu, A., Juan, A.C.: Deconvolutional networks for point-cloud vehicle detection and tracking in driving scenarios. In: Mobile Robotics, 2017. (ECMR-2017). Eur. Conf. on. IEEE (2017)
  ```

# 2. Related Work


## 2.1 Object Detection in Lidar Point Clouds.

- 오래된 접근법은 클러스터링 알고리즘을 이용하여 세그멘테이션 후 각 그룹별로 Class를 적용 하는 것이다. `Classic approaches for object detection in lidar point clouds use clustering algorithms to segment the data, assigning the resulting groups to different classes [2, 27, 6, 18]. `

  ```
  2. Arras, K.O., Mozos, O.M., Burgard, W.: Using boosted features for the detection of people in 2d range data. In: Robotics and Autom., 2007 IEEE Int. Conf. on, pp. 3402–3407. IEEE (2007)
  27. Vaquero, V., Repiso, E., Sanfeliu, A., Vissers, J., Kwakkernaat, M.: Low cost, robust and real time system for detecting and tracking moving objects to automate cargo handling in port terminals. In: Robot 2015: 2nd Iber. Robotics Conf., pp. 491–502. Springer (2016)
  6. Douillard, B., Underwood, J., Kuntz, N., Vlaskine, V., Quadros, A., Morton, P., Frenkel, A.: On the segmentation of 3d lidar point clouds. In: Robotics and Autom. (ICRA), 2011 IEEE Int. Conf. on, pp. 2798–2805. IEEE (2011)
  18. Mertz, C., Navarro-Serment, L.E., MacLachlan, R., Rybski, P., Steinfeld, A., Suppe, A., Urmson, C., Vandapel, N., Hebert, M., Thorpe, C., et al.: Moving object detection with laser scanners. J. of Field Robotics 30(1), 17–43 (2013)
  ```


- 또 다른 접근법은 사전 정보(environment structure)를 이용하여 세그멘테이션과 글러스터링을 쉽게 하는 것이다. `Other strategies, such as the one used as baseline method in this paper, benefit from prior knowledge of the environment structure to ease the object segmentation and clustering [20, 24]. `

  ```
  20. Petrovskaya, A., Thrun, S.: Model based vehicle detection and tracking for au- tonomous urban driving. Autonomous Robots 26(2-3), 123–139 (2009)
  24. Teichman, A., Levinson, J., Thrun, S.: Towards 3d object recognition via classification of arbitrary object tracks. In: Robotics and Autom. (ICRA), 2011 IEEE Int. Conf. on, pp. 4034–4041. IEEE (2011)
  ```


- 3D 복셀은 주변 점들을 그룹핑 하여 연산 부하를 줄이기 위한 용도로 탄생하였다. 복셀의 최상위 부터 그래프를 생성하여 분류 작업을 진행 한다. `3D voxels can be also created to reduce computational costs by grouping sets of neighbor points. Graphs can be later built on top of grouped voxels to classify them in objects [30, 25, 19]. `

  ```
  30. Wang, D.Z., Posner, I., Newman, P.: What could move? finding cars, pedestrians and bicyclists in 3d laser data. In: Robotics and Autom. (ICRA), 2012 IEEE Int. Conf. on, pp. 4038–4044. IEEE (2012)
  25. Triebel, R., Shin, J., Siegwart, R.: Segmentation and unsupervised part-based dis- covery of repetitive objects (2010)
  19. Papon, J., Abramov, A., Schoeler, M., Worgotter, F.: Voxel cloud connectivity segmentation-supervoxels for point clouds. In: Proc. of the IEEE Conf. on Comput. Vis. and Pattern Recognit. (CVPR), pp. 2027–2034 (2013)
  ```

- 좀더 최근의 접근법은 spin images, shape models, geometric statistics와 같은 hand-crafted 특징들을 추출 할수 있다. `More recent methods are able to process the point cloud space (raw, or reduced in voxels) to extract hand-crafted features such as spin images, shape models or geometric statistics [3]. `

  ```
  3. Behley, J., Steinhage, V., Cremers, A.B.: Performance of histogram descriptors for the classification of 3d laser range data in urban environments. In: Robotics and Autom. (ICRA), 2012 IEEE Int. Conf. on, pp. 4391–4398. IEEE (2012)
  ```


- Vote3D는 이러한 sparse한 포인트 클라우드에 다른 특징 정보를 추가 하여 사용 하였다. `Vote3D [29] uses this second approach and encodes the sparse lidar point cloud with different features. `
    - 결과물에 대하여 서로 다른 크기의 3D 슬라이딩 윈도우를 이용하여 스캔후 SVM을 이용하여 식별하였다. `The resulting representation is scanned in a sliding manner with 3D windows of different sizes, and an SVM followed by a voting scheme is used to classify the final candidate windows`

## 2.2 Deep Learning for Object Detection on Lidar information.

- 초기 접근은 CNN을 바로 적용 하였다. `Some early approaches on using CNNs to detect vehicles over 3D lidar point clouds make use of 3D convolutions [14] or sparse 3D convolutions acting as voting weights for predicting the detection scores [8, 10]. `

- 하지만, Lidar 포인트클라우드의 특징(고차원, 희박성)으로 인하여 연산 부하가 크다. `However, due to the high dimensionality and sparsity
of 3D lidar data, deploying them over point clouds implies high computational burden.`

- 또다른 접근법은 3D 포인트 클라우드를 2D representation으로 바꾸어 2D CNN을 적용 한다. `Another adopted approach is to apply the well know 2D convolution tools over equivalent 2D representations of the 3D point cloud. `

- In this way, [15] predicts the objectness of each point as well as vehicle 3D bounding boxes by applying a Fully Convolutional Network over a front view representation in which each element encodes a ground-measured distance and height of the corresponding
3D point.

  ```
  15. Li, B., Zhang, T., Xia, T.: Vehicle detection from 3d lidar using fully convolutional network. arXiv preprint arXiv:1608.07916 (2016)
  ```

The recent evolution of [15] combines RGB images with lidar information to generate accurate 3D bounding box proposals, obtaining state of the art results in the detection challenge of the Kitti dataset [5].
  - However, this method does not fulfill the lidar-only requirement that we impose in our work.

```
5. Chen, X., Ma, H., Wan, J., Li, B., Xia, T.: Multi-view 3d object detection network for autonomous driving. arXiv preprint arXiv:1611.07759 (2016)
```

# 3. System Description


- 구성
  1. an initial preprocessing step of the lidar information
  2. a convolutional network performs per-point vehicle detection, which results are later used to obtain bounding boxes of vehicle proposals.
  3. using as additional input the ego-odometry, these vehicle proposals are tracked through time, obtaining information about their poses, dimensions and velocities.

## 3.1 Data Arrangement

Kitti 데이터셋에서 GT는 앞면 이미지에만 있으므로, 3D 데이터를 이와 같은 앵글로 변경

As the Kitti tracking benchmark provides only labels for the elements within the front camera field of view, we restrict our 3D point cloud to the corresponding angles.

The remaining points are then transformed for the elements within the front camera field of view, we restrict our 3D point cloud to the corresponding angles.

## 3.2 Convolutional Network for Lidar Vehicle Detection

전면 이미지의 2D변환 후 CNN기반 분류

## 3.3 Bounding Box Extraction and Matching


## 3.4 Lidar-based Vehicle Tracking

이전 연구에서 했던 방식처럼 2D로 변경후 MH-EKF 사용하여 추적 수행

The tracking system has been implemented following the same 2D approach that in our previous work [26], which results in a reasonable simplification since wheeled vehicles transit on the road plane.
