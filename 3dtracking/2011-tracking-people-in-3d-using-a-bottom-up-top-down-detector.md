|논문명 |Tracking People in 3D Using a Bottom-Up Top-Down Detector |
| --- | --- |
| 저자\(소속\) | L.Spinell\(\) |
| 학회/년도 | ICRA2011, [논문](http://www2.informatik.uni-freiburg.de/~spinello/spinelloICRA11.pdf) |
| Citation ID / 키워드 | multi-hypothesis tracking, Jump Distance Clustering |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | [홈페이지](http://www2.informatik.uni-freiburg.de/~spinello/ICRA2011.html) , [Youtube](https://www.youtube.com/watch?v=WyQ9yRtDmkU&feature=youtu.be)|
| 코드 | - |


|년도|1st 저자|논문명|코드|
|-|-|-|-|
|2010|L.Spinell|[A Layered Approach to People Detection in 3D Range Data](http://www2.informatik.uni-freiburg.de/~spinello/spinello10layered.pdf)|-|
|2011|L.Spinell|[**Tracking People in 3D Using a Bottom-Up Top-Down Detector**](http://www2.informatik.uni-freiburg.de/~spinello/spinelloICRA11.pdf)|-|


# Tracking People in 3D Using a Bottom-Up Top-Down Detector (40%)


In our approach, a **top-down classifier** selects hypotheses from a **bottom-up detector**, both based on sets of boosted features.

- The bottom-up detector learns a layered person model from a bank of specialized classifiers for different height levels of people that collectively vote into a continuous space.

- In the top-down step, the candidates are classified using features that are computed in voxels of a boosted volume tessellation.


 ## I. Introduction

본 논문에서는 Lidar를 통해 사람 탐지/추적에서 발생하는 2개의 문제점을 기술한다. `In this paper we address two problems, detecting people in 3D range data and tracking people in 3D space. `

이전 연구 [1] 대비 추적 기능과 top-donw절차가 추가 되었다. `We extend our previous work on 3D people detection [1] by the tracking stage and an additional top-down procedure in the detection pipeline. `

```
[1] L. Spinello, K. O. Arras, R. Triebel, and R. Siegwart, “A layered approach to people detection in 3D range data.” in AAAI Conf. on Artif. Intell. (AAAI), 2010.
```

이 기능은 먼거리에서 탐지되는 sparsely한 센싱으로 인한 오류를 줄어 준다. `This procedure aims at reducing false positives that typically occur with sparsely sampled individuals at large distances from the sensor. `

또한, 탐지와 추적 기능을 합쳤다. `We further combine detection with tracking and present results from a tracker this is able to estimate the motion state of multiple people in 3D. `

이를 위해서 **MHT 기법** 을 적용 하였다. `To this end, we employ a multi-hypothesis tracking approach (MHT) by Reid [2] and Cox et al. [3]. `

```
[2] D. B. Reid, “An algorithm for tracking multiple targets,” IEEE Transactions on Automatic Control, vol. 24, no. 6, pp. 843–854, 1979.
[3] I. J. Cox and S. L. Hingorani, “An efficient implementation of reid’s multiple hypothesis tracking algorithm and its evaluation for the purpose of visual tracking,” IEEE Trans. Pattern Anal. Mach. Intell. (PAMI), vol. 18, no. 2, pp. 138–150, 1996.
```

성능평가를 위해 다른 연구들과 비교 하였다. `In the experiments we compare our approach with related techniques for detection in 3D range data, in particular spin images [4] and template- based classification. `

```
[4] A. Johnson and M. Hebert, “Using spin images for efficient object recognition in cluttered 3d scenes,” IEEE Trans. on Pattern Analysis & Machine Intell., vol. 21, no. 1, pp. 433 – 449, May 1999.
```

### 관련 연구

3D 기반 사람 탐지는 많이 연구 되지 않았다. 대부분은 2D range data를 이용한 것들이다. `While there is little related work for people detection and tracking in 3D, many researchers addressed this task using 2D range data. `


초창기 연구에서는 moving local minima를 활용하는 에드혹 분류기를 사용하였다. `In early works [5], [6], [7], people are detected using ad-hoc classifiers, looking for moving local minima in the scan. `

```
[5] B. Kluge, C. K¨ohler, and E. Prassler, “Fast and robust tracking of multiple moving objects with a laser range finder,” in Int. Conf. on Rob. & Autom. (ICRA), 2001.
[6] A. Fod, A. Howard, and M. Matar´ıc, “Laser-based people tracking,” in Int. Conf. on Rob. & Autom. (ICRA), 2002.
[7] D. Schulz, W. Burgard, D. Fox, and A. Cremers, “People tracking with a mobile robot using sample-based joint probabilistic data association filters,” Int. Journ. of Rob. Research, vol. 22, no. 2, pp. 99–116, 2003.
```

최초의 학습 기반 방식은 [8]에서 시작 되었다. 이 방식은 2D 포인트 클라우드를 학습 분류 하였다. `The first principled learning approach has been taken by Arras et al. [8] where a classifier for 2D point clouds has been learned by boosting a set of geometric and statistical features. `

```
[8] K. O. Arras, O. Mart´ınez Mozos, and W. Burgard, “Using boosted features for the detection of people in 2d range data,” in Int. Conf. on Rob. & Autom. (ICRA), 2007.
```

2D range 방식은 한계가 있어서 이후 연구자들은 **multiple co-planar 2D laser** 스캐너를 사용하는 방법을 제안 하였다. `As there is a natural performance limit when using only a single layer of 2D range data, several authors have been using multiple co-planar 2D laser scanners [9], [10], [11]. `

```
[9] S. Gidel, P. Checchin, C. Blanc, T. Chateau, and L. Trassoudaine, “Pedestrian detection method using a multilayer laserscanner: Appli- cation in urban environment,” in Int. Conf. on Intel. Rob. and Sys. (IROS), 2008.
[10] A. Carballo, A. Ohya, and S. Yuta, “Fusion of double layered multiple laser range finders for people detection from a mobile robot,” in IEEE Int. Conf. on Multisensor Fusion and Integration for Intelligent Systems (MFI), 2008.
[11] O. M. Mozos, R. Kurazume, and T. Hasegawa, “Multi-part people detection using 2d range data,” International Journal of Social Robotics, vol. 2, no. 1, 2010.
```


3D를 이용한 연구는 [12]에서 3D데이터를 **virtual 2D slice** 로 변환하여 SVN을 이용하여 지면위의 **salient(핵심적인) vertical objects** 를 탐색하게 하였다. `In the field of people detection in 3D data, Navarro et al. [12] collapse the 3D scan into a virtual 2D slice to find salient vertical objects above ground. `
- They align a window to the principal data direction, compute a set of features, and classify pedestrians using a set of SVMs.


```
[12] L. Navarro-Serment, C. Mertz, and M. Hebert, “Pedestrian detection and tracking using three-dimensional ladar data,” in Int. Conf. on Field and Service Robotics, 2009.
```

[13]에서는 스테레오 비젼을 통해 습득한 포인트 클라우드를 이용하여 geometrical/statistical features와 고정된 사람 모델(키, 넓이??)을 이용해 사람을 탐지 하였다. `Bajracharya et al. [13] detect people in point clouds from stereo vision by processing vertical objects and considering a set of geometrical and statistical features of the cloud based on a fixed pedestrian model.`

```
[13] M. Bajracharya, B. Moghaddam, A. Howard, S. Brennan, and L. Matthies, “Results from a real-time stereo-based pedestrian detec- tion system on a moving vehicle,” in Workshop on People Detection and Tracking, IEEE ICRA, 2009.
```


위 두 방식[12,13]은 모두 Top-down 탐지 방식으로 볼수 있다. `Both of them can be seen as top-down detection procedures.`

### 본 논문의 방식

본 논문에서는 최신 기술들을 확장 하여 사용하였다. `Our approach extends the state-of-the-art in several aspects. `

1. First, all these works require a ground plane assumption which prevents them from being true 3D methods. This is not required in our case.
  - We combine a top-down classifier with a bottom-up detector and quantify the improvement of this combination.


2. We then compare our method to two established 3D object detection techniques, **spin images** and **template-based** classification,
  - and demonstrate that with equal error rates (EER) of at least 93% for people up to 20m afar, our approach clearly outperforms the alternative techniques.


3. Finally, we combine our detector with 3D tracking.


논문의 구성
1. the combined bottom-up top-down detection approach is presented in the next section including the learning and the classification phase.
2. Tracking is described in Section IV.
3. Section V contains quantitative comparisons and experimental results and
4. Section VI concludes the paper.

## II. The bottom-up approach to 3D people detection

이전 연구[1]결과인 **bottom-up detector** 에 대하여 살펴 보겠다. `In this section we briefly summarize the bottom-up detector from [1]. `

용어 정리 `Let us first define the terms.`
  - **By bottom-up** we denote the _myopic scheme_ thats starts with local segments of 2D range data and works up to a detection hypothesis in 3D.
  - **By top-down** we mean the procedure that begins with a predefined volume in 3D and the totality of data within that volume and works down to a classification of these data.

이러한 방식을 사용하는 이유는 3D range 에서 얻는 데이터는 **슬라이스** 나 **2D line** 이다.  `The idea of the method presented in [1] follows the observation that most 3D range finding devices acquire 3D point clouds in slices or lines of (typically non-coplanar) 2D data. `

이점을 착안 하여 기존의 2D range에서 사용한 방법을 활용하여 사람을 탐지 하고 이를 합쳐서 3D 탐지기로 만들었다. `This enables us, in a first step, to reuse known and proven techniques for detecting people in 2D range data that then are combined to a 3D detector.`

### A. The learning phase
