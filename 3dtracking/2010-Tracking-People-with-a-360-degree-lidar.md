| 논문명 | Tracking People with a 360-Degree Lidar |
| --- | --- |
| 저자\(소속\) | John Shackleton\(\) |
| 학회/년도 | 2010, [논문]() |
| Citation ID / 키워드 |  |
| 데이터셋\(센서\)/모델 |  |
| 관련연구 |  |
| 참고 |  |
| 코드 |  |

# Tracking People with a 360-Degree Lidar

## 1. Introduction

* 목적
  * segmenting the scene into targets of interest,
  * classifying the segmented point cloud into those segments that are human,
  * correlating tracks with established targets,
  * tracking the targets from frame to frame.

## 2. Technical Approach

* 절차
  * segmentation and classification requires grouping
  * separating points \(or voxels\) of the point cloud into objects that are
    * irrelevant,
    * matched with existing targets,
    * or identified as new targets

* 챌린지 `three failure modes became the most apparent:`
  * \(2.1\) classification and matching errors between multiple human targets,
  * \(2.2\) segmentation errors between humans and fixed objects in the scene,
  * \(2.3\) and segmentation errors between targets that are very close together.

> 다음장에서 각 챌리지에 대하여 다룬다.

### 2.1. Classification and Matching Humans

Our approach takes advantage of two characteristics of lidar data.

* First, the human target has a `unique signature` formed by the curvature of its surface.
* Second, since a new point cloud is generated at 10Hz, target information `accumulated` from a previous frame can facilitate and validate target detection in subsequent frames.

#### 2.1.1 Surface Matching

* Our implementation settles upon a surface matching technique called `spin images`,

* 정의 : collects a set of contour descriptions local to each vertex on an object’s surface

* 스핀이미지가 3D 데이터 처리에 좋은 이유 `Spin images are a good fit for 3D real-time point clouds because`

  * localized patches로 표현 방식을 변경 하여 **occlusions** 문제를 잘 해결 한다. `they handle occlusions very well, since they reduce the surface representation to a set of localized patches.`
  * 상대적으로 성능이 좋다. `Spin images are also relatively efficient, especially compared to other surface matching techniques developed for applications with static scenes that are not real-time constrained.`

![](https://i.imgur.com/1HilF5m.png)

본 논문에서는 **surface matching** 를 Tracking을 위해 사용 하였다. `We utilize surface matching for lidar tracking as follows.`

절차

1. 공간 정보를 기반으로 그룹핑 `A group of points is initially segmented based on spatial separation using 3D occupancy grids over the scene.`

2. 간단한 규칙 기반으로 후보군\(사람\) 구분 `Point groups are considered candidate human targets based on simple constraints of dimensions and orientation.`

3. 후보군들에 대해 **스핀 이미지** 생성 `For potential human targets, a spin image map is constructed.`

4. 다음 프레임 생성시 각 후보군의 이전 스핀 이미지와 새로 생성된 스핀 이미지를 비교 한다. `As consecutive frames are generated, spin image maps of new potential targets are compared to the spin image maps of previously identified targets, using the correlation formula described in [6].`

1. 상관관계 점수가 좋으면 Match된것으로 간주 한다. `When a new track has a correlation score that compares well enough with a prior target, then a match is declared.`
   * Match가 되면 업데이트 한다. `When a match is detected the spin image map of the target is updated with the latest surface descriptions of the track, and the target is tracked for another frame.`
   * Match가 안되면, 새 타겟으로 지정된다. `Tracks that do not match an existing target, and meet the dimensional constraints of a human, are identified as new targets.`

1. We could also use spin images to derive a set of templates representing various human shapes, which in turn can be used to classify new targets.

2. For this initial work, however, we defer template-matching classification and use simple dimensional characteristics to identify new targets.

#### 2.1.2 Tracking-Aided Classification

* 스핀 이미지를 수백개의 타겟과 비교 하는것은 비 효율적인 작업이다. `It would be inefficient to perform spin image comparisons against all existing targets in a scene, potentially hundreds of targets.`

* 따라서 EKF를 이용하여 타겟의 위치를 에측 하였다. `Consequently, we employ an extended Kalman filter (EKF) to estimate the position of a target from one frame to the next [7].`

* 이후 근처에 있는 대상에 대하여서만 수행 한다. `Surface matching is then limited to the comparison of potential targets of the current frame against the spin image signatures near known tracks.`

* 스핀이미지의 **상관관계 점수** 는 예측된 거리 정보를 기반으로 아래 공식으로 보정될수 있다. `The spin image correlation score for each comparison is thus refined to include the distance of the current track position from the estimated position of the established target, as shown in Eq. (1)`

> 자세한 식 및 설명은 논문 참고

#### 2.1.3 Uneven Point Density

* 스핀 이미지 알고리즘 사용시 각 point들은 동일한 간격을 두고 있어야 하는 가정 사항이 있다.`A key assumption is that adjacent 3D points on an object’s surface are approximately equidistant from each other.`

* 하지만 Lidar의 특성상 이 가정사항을 만족 할수 없다.

* 해결책 : Instead, we compensate by

  * interpolating a mesh of equidistant segments over the raw points of the potential target.
  * The length of the segments is a function of the linear distance between the object and the lidar sensor.
  * The technique we use to build the mesh is described in \[9\].

```
[9] Hoppe, H. “Surface Reconstruction from Unorganized Points”. PhD Thesis, Dept. of Computer Science and Engineering, University of Washington, June 1994.
```

### 2.2. Segmentation and the Background Scene

![](https://i.imgur.com/iACrw7X.png)

* 에러의 대부분은 배경 처리때문이다. `A high number of tracking errors and false-positives with 360-degree lidars are related to the interaction of the people and the background scene.`

* 예를 들어, `For example,`

  * 벽 옆에 있는 사람을 벽으로 인식 한다. `people who stand next to the wall are often mistaken for the wall.`
  * 그림자를 만들어서 발생하는 문제점 `Another key observation is that people cast lidar shadows, a transient, moving patch devoid of points in the scene created when a moving object passes in front of a fixed object (Figure 3).`

* 해결책은 고정된 물체를 비인간, 지면, 벽, 가구로 인식하고 제거 하는것이다. `Both of these problems are addressed by eliminating from each frame the persistent(끈질) static objects that are known to be non-human, such as the ground, walls, and furniture.`
  * 2D 이미지 처리에서는 이 기술을 **배결제거** 라고 한다. `In 2D image processing, this technique is known as background subtraction.`

##### \[3D background subtraction\]

![](https://i.imgur.com/exvHOYc.png)

* 본 논문에서는 separate occupancy grid를 static objects로 populating함으로써 배경을 제거 하였다. `We perform 3D background subtraction by populating a separate occupancy grid with static objects.`

* The cells of the occupancy grid form our background mask.

* 각 셀은 최근 occupancy를 기록하고 있다. `Each 3D cell also includes a history buffer that records its recent occupancy, represented as a string of bits (eight bits in our implementation).`

* 절차  
  1. Initially all cells are marked as empty and all bits are set to zero.  
  2. Periodically we sample a frame of lidar data, and for each voxel in the frame we calculate which cell of the background mask it occupies.  
  3. For each occupied cell, we set the highest order bit.  
  4. Before sampling another frame, the background mask is aged, so that the lowest order bits of each cell’s mask are shifted one place.

* To determine which cells represent the static background, each cell in the scene’s background mask is examined.

* A cell is marked as static background if a majority of its bits are set.

* A persistently empty space will have all bits in its cell mask unset.

* After sampling a minimum number of periodic frames, the learned background mask is applied continuously as a filter for future frames.

* A point in subsequent frames is discarded if it occupies a background cell.

> 이 방법을 통해 90%까지 입력 데이터를 줄일수 있다. `In practice, this approach reduces the lidar input data by as much as 90% (Figure 4).`

* 이 방식은 부가적인 효과도 있다. `This approach yields other benefits as well.`
  * First, it greatly simplifies segmentation, since most of points that are not marked as background are usually objects of interest.
    * Segmenting people standing near walls is much simpler when the walls are removed.
  * Second, transient artifacts such as lidar shadows are automatically removed without further processing.

### 2.3. Segmenting Close Groups of People Some

* 붙어 있는 사람을 분석하는것은 어려운 문제 이다.

* 표면 매칭 방식이 휴먼 타겟 조각들의 모호성을 없애주기는 하지만, 이 작업을 위해서는 선행적으로 두 물체가 적절하게 세그멘테이션 되어 있어야 한다. `While surface matching can disambiguate patches of human targets, reliable surface matching comparisons within real-time lidar data cannot take place until after the human targets are first properly segmented into separate objects.`

* For example, if multiple tracks in close proximity are incorrectly segmented into a single object, such as two people shaking hands \(Figure 5\), the resulting surface description does not contain sufficient detail to identify the separate tracks within the same.

* Moreover, sampling of correlation points of a multi-track object will likely include an unordered mixture of points from each of the tracks, and therefore will not capture a surface description that separates the multiple tracks properly.

* Therefore, false negatives during tracking will occur.

* 따라서 분리된 오브젝트는 최대 한개의 트랙만 가지고 있어야 한다. `Thus, a segmented object should contain at most one track.`

* 오브젝트에 한개 이상의 트랙이 발생하는데에는 아래의 3가지 이유일수 있다. `Three kinds of events can lead to an object with more than one track:`

  * 1\) separate established targets can come together in close proximity,
  * 2\) new tracks can enter a scene together in close proximity, and
  * 3\) a hybrid event, such as a new track that was previously occluded first appears within a close group of existing tracks.

> 이후 이 3가지 시나리오에 대하여 두가지 군집화 알고리즘\(K-mean, DBSCAN\)을 이용하여 해결

* 클러스터링 기법이 3D 포인틀르 세그멘테이션 하는데 일반적인 방법이다. `Clustering is a common technique to segment 3D points in space with many algorithms and variations to choose from [10].`

```
[10] Xu, R., Wunsch, D. “Survey of Clustering Algorithms”. IEEE Transactions on Neural Networks, Vol. 16, No. 3. pp 645-678. May 2005.
```

* 본 논문에서는 2개의 군집화 알고리즘을 적용 하였다. `Our solution applies two common clustering algorithms, to objects of a certain minimum size that may contain more than one track.`

  * K- means clustering \[11\], \[12\]
  * DBSCAN clustering \[13\]

* 두 알고리즘 적용을 위해서 3D 포인트는 X-Y좌표\(Top-Down View\)로 클러스터링 되었다. `For both clustering algorithms, the 3D points of the larger object are clustered in the x-y plane, i.e., the top-down view.`

#### \[K-means\]

위 3가지 발생 가능한 시나리오 중에서 1번째

* For the first case, K-means is used when known targets come together into a single larger object.

* The algorithm is seeded with the number of expected clusters \(tracks\) and an initial guess for the centroid point of each cluster, which are the estimated x-y midpoints generated by the Kalman filter.

* The K-means clustering iterates recursively over the points in the object until convergence is reached and all the points are assigned to a new cluster subdivided from the original object.

* The new \(smaller\) objects are then treated as any other potential track in the system, ready for classification.

* Clusters that do not have enough points for surface matching are discarded.

#### \[DBSCAN\]

위 3가지 발생 가능한 시나리오 중에서 2,3번째

* The other two scenarios are less predictable, because we have less confidence as to the number of tracks bundled into the larger object.

* Thus, we switch to DBSCAN clustering when the number of human tracks within an object is unknown.

* We tried an approach that exclusively used DBSCAN, but it was not reliable enough.

* For example, if two people are shoulder to shoulder, the DBSCAN approach often clusters the two tracks into a single object, while K-means is able to identify the separate tracks when their existence is established in prior frames.

Certainly many other clustering algorithms are suitable for segmenting the point cloud, each perhaps optimal in specific situations.

## 2.4. Kalman Filter Details

an extended Kalman filter estimates the frame-by-frame position of each person

* 3D position
* 3D velocity
* 1D heading direction

```
[7] Ramachandra, K.V. Kalman Filtering Techniques for Radar Tracking. CRC, 2000.
```

---

# \[참고\] Spin Image

| ![](https://i.imgur.com/LeodTbl.png) | ![](https://i.imgur.com/OHADzeH.png) |
| --- | --- |


* 3D 형태 기술자, Object recognition에 활용 가능

* 절차

  * 기준점 주변에 사수의 겹치지 않은 원통\(반원\)으로 나눔
  * 각 원통의 Point 수를 개산
  * 시각화

> 참고 : [Spin-Images: A Representation for 3-D Surface Matching](https://www.ri.cmu.edu/publications/spin-images-a-representation-for-3-d-surface-matching/), [Spin Images](http://homepages.inf.ed.ac.uk/rbf/CVonline/LOCAL_COPIES/AV0910/SpinImages.pdf), \[논문\_2012\] 각 분할 스핀영상을 사용한 3차원 얼굴 특징점 검출 방법,



