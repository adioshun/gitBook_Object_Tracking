CHANGE DETECTION OF MOBILE LIDAR DATA USING CLOUD COMPUTING

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

### 2.2 multi-data octree

An out-of-core method was developed in [Richter et al., 2013] for detecting changes in massive point clouds without having to reduce the raw point data. 

The basic idea of the method is computing the distance between each point to its closest point. 

This distance attribute is used to characterize the amount of geometry change. 

To computing the distances efficiently, a specialized data structure multi-data octree is employed. 

Multi-data octree, which is developed based on octree, can manage 3D point clouds in outof-core storage. 

It endows the method with the ability to process a large amount of data which can not fit memory. 

However, for each comparison, a multi-data octree has to be constructed. 

In addition, the implementation of the data structure is not as straightforward as voxel grid used in our platform

### 2.3 reviewe 논문 

Recent approaches on change detection in laser scan data were reviewed in [Lindenbergh and Pietrzyk, 2015]. 

주요 문제점 언급 `Major existing difficulties are studied including `
- local varying properties of point cloud, 
- registration, 
- varying view points during acquisition, 
- and temporary objects. 

분류 : In the report, methods are categorized into two groups. i.e., 
1. pure binary change detection methods and 
2. detection methods that quantify changes. 


버드아이뷰 방식의 탐지법 : Readers can also refer to [Xiao et al., 2015] for a brief overview on change detection methods from different fields such as remote sensing and photogrammetry, computer vision, and robotics.

본 논문의 방식 
- Our method is similar to the approach proposed in [Barber et al.,2008] which is based on an octree. 
- On the other hand, we employ a voxel grid and implement entire method by means of cloud computing. 
- The differences between an octree and a voxel grid and the reasons of applying a voxel grid in our work are further
investigated in Section 3.2














