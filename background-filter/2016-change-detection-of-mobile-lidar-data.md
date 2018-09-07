CHANGE DETECTION OF MOBILE LIDAR DATA USING CLOUD COMPUTING  2016

https://www.int-arch-photogramm-remote-sens-spatial-inf-sci.net/XLI-B3/309/2016/isprs-archives-XLI-B3-309-2016.pdf


## 1. INTRODUCTION

어려운 이유 `Change detection of LiDAR data is still quite difficult although many methods have been proposed over the last few decades [Memoli and Sapiro, 2004, Richter et al., 2013, Lindenbergh and ´Pietrzyk, 2015]. `

1. First, LiDAR data is a discrete format by sampling on continuous object surfaces, and thus surface reconstruction
[Kazhdan et al., 2006] is often required. 

2. Second, different types of errors are inevitable such as missing points caused by blocking and misalignment in point cloud registration. 
    - Moreover, data sets acquired using different devices can vary in sampling density and distribution. 

3. Last but not least, the methods should be efficient enough to compensate for the increasing data volume.


In this paper, we present a method using cloud computing technologies to address the problem of change detection in the context of big data
- proposing an efficient method to detect changes in mobile LiDAR data,
- demonstrating the great potential of Apache Spark on large LiDAR data processing.


## 2. RELATED WORK

### 2.1 based on Gromov-Hausdorff distance

A theoretical and computational framework has been proposed in [Memoli and Sapiro, 2004] for comparing point clouds. 

The underlying framework is based on Gromov-Hausdorff distance and embedded in a probabilistic setting. 

Gromov-Hausdorff distance generalizes Hausdorff distance to compare two compact metric spaces with respect to all isometric embedding. 

Therefore, the framework can compare two point clouds using certain isometric deformation. 

However, computing a discrete approximation of Gromov-Hausdorff distance is not straightforward. 

Pairwise geodesic distances between points are required, which introduces efficiency issue.

```
Memoli, F. and Sapiro, G., 2004. Comparing point clouds. In: ´Proceedings of the 2004 Eurographics/ACM SIGGRAPH symposium on Geometry processing, ACM, pp. 32–40.
```


### 2.2 multi-data octree

An out-of-core method was developed in [Richter et al., 2013] for detecting changes in massive point clouds without having to reduce the raw point data. 

```
Richter, R., Kyprianidis, J. E. and Dollner, J., 2013. Out-of-core gpu-based change detection in massive 3d point clouds. Transactions in GIS 17(5), pp. 724–741.
```

The basic idea of the method is computing the distance between each point to its closest point. 

This distance attribute is used to characterize the amount of geometry change. 

To computing the distances efficiently, a specialized data structure multi-data octree is employed. 

Multi-data octree, which is developed based on octree, can manage 3D point clouds in outof-core storage. 

It endows the method with the ability to process a large amount of data which can not fit memory. 

However, for each comparison, a multi-data octree has to be constructed. 

In addition, the implementation of the data structure is not as straightforward as voxel grid used in our platform

### 2.3 reviewe 논문 

Recent approaches on change detection in laser scan data were reviewed in [Lindenbergh and Pietrzyk, 2015]. 

```
Lindenbergh, R. and Pietrzyk, P., 2015. Change detection and deformation analysis using static and mobile laser scanning. Applied Geomatics 7(2), pp. 65–74.
```

주요 문제점 언급 `Major existing difficulties are studied including `
- local varying properties of point cloud, 
- registration, 
- varying view points during acquisition, 
- and temporary objects. 

분류 : In the report, methods are categorized into two groups. i.e., 
1. pure binary change detection methods and 
2. detection methods that quantify changes. 


버드아이뷰 방식의 탐지법 : Readers can also refer to [Xiao et al., 2015] for a brief overview on change detection methods from different fields such as remote sensing and photogrammetry, computer vision, and robotics.

```
Xiao, W., Vallet, B., Bredif, M. and Paparoditis, N., 2015. Street environment change detection from mobile laser scanning point clouds. ISPRS Journal of Photogrammetry and Remote Sensing
107, pp. 38–49.
```


본 논문의 방식 
- Our method is similar to the approach proposed in [Barber et al.,2008] which is based on an octree. 
- On the other hand, we employ a voxel grid and implement entire method by means of cloud computing. 
- The differences between an octree and a voxel grid and the reasons of applying a voxel grid in our work are further
investigated in Section 3.2




## 3. OUR METHOD


### 3.1 Problem Statement

we have two LiDAR data collections of the same city region which are captured at different dates even using different mobile mapping systems. 
- 기준 데이터, The earlier acquired data set is chosen as the reference,
- 타겟 데이터, and the newer one is selected as the target. 

Change detection is performed to obtain differences in the target regarding the reference


The proposed method 
1. takes the two point clouds as inputs, 
2. performs difference detection, and assigns a label to each point. 
3. The outputs of the method are two sets (수식 참고)

### 3.2 Algorithm for Difference Detection

the input of our method are two point clouds without further assumption such as sampling density and distribution. 

The aim of our method is to compute geometry differences between the input point clouds.

The algorithm for difference detection is outlined in Figure 1.

![](https://i.imgur.com/p2c0RK2.png)
```
Figure 1. The figure outlines the algorithm to compare the geometry of two point clouds. 
- A voxel grid is built based on the point clouds.
- Geometry differences of the point clouds can be computed by comparing occupancy status of each voxel with respect to the two point clouds. 
- The rightmost column visualizes the computed geometry differences which are illustrated as orange dots in the figure.
```

Given the input point clouds P1 (green) and P2 (red), a voxel grid is built. 

A voxel grid, which is a regular grid in three dimensional space, is popularlly used in computer graphics, especially
in 3D reconstruction [Curless and Levoy, 1996] and rendering [Fujimoto et al., 1986]. 

To construct the grid, the minimum bounding box of the two point clouds is computed first and then the box is partitioned regularly by voxels within the same size. 

In our algorithm, the voxel size is a parameter prescribed by users to control the resolution of detected geometry differences. 

A voxel v is occupied by point cloud P if and only if some point p ∈ P is located in the voxel v. 

Furthermore, an occupied voxel v must be one of the three following cases:
1. occupied by P1 only,
2. occupied by P2 only,
3. occupied by both P1 and P2.


In our algorithm, a label l is assigned to each point p by checking such occupancy information.

In our algorithm, point clouds are transformed into voxels as an intermediate geometry representation. 

Mesh reconstruction [Kazhdan et al., 2006] and Hausdorff distance computation [Memoli and Sapiro, 2004] are successfully avoided by virtue of voxels, which makes our algorithm efficient. 

Voxel grid can be considered as a space partitioning scheme as well. 

In a voxel grid, voxels have the constant size. Such size can be prescribed as a parameter by users. 

Voxel octree [Laine and Karras, 2011] is another popular partitioning scheme. 

Contrary to voxel grid, voxels from a voxel octree may have different sizes. 

In our algorithm voxel grid is applied instead of voxel octree, because voxel grid can perform a uniform resampling spontaneously due to constant voxel size, which makes our algorithm robust to varying sampling densities. 

In addition, voxel grid is more suitable for our parallel computing engine Apache Spark. 




