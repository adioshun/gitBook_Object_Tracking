Person Tracking and Following with 2D Laser Scanners

http://digitool.library.mcgill.ca/webclient/StreamGate?folder_id=0&dvs=1535431430325~699

석사 학위 82page



# 2D tracking

## 1. 


## 2. Background

### 2.1 ROS

### 2.2 Occupancy Grid Mapping

### 2.3 Target Tracking


Target tracking is the process of **estimating the pose**(=위치, 방향) of one or many objects based on noisy observations from a sensor.

#### A. The Kalman Filter

In the case of state estimation of a single tracked target with noisy observations, a Kalman filter can provide an **estimate of the target’s state** which is more accurate than any single observation alone [35]. 

#### B. Data Association

칼만필터는 단일 물체의 state estimation에는 유용한 툴이다. `The Kalman filter is a useful tool for state estimation of a single target where observations are known unambiguously to have originated from the target. `

하지만, 다중 물체에서는 DA 기법이 필요 하다. However, in the case of multiple tracked targets, a data association method is required.
- multiple tracked targets: where observations can originate from all targets and ambiguity exists regarding which target produces which observation,

Formally, data association is concerned with finding a correspondence between 
- a given set of previously tracked objects (=tracks) $$X_{k−1}$$ and 
- a set of detections, or observations, in the current timestep $$Z_k$$.

This assignment can then be used to obtain an updated set of tracks $$X_k$$ by performing a measurement update on each track using its assigned observation, as is shown in Kalman filter framework.


###### [In the simplest case]

the number of tracks always equals the number of detections per timestep and there exists a one-to-one mapping between the two. 

###### [More complicated cases arise] 

for example, when new objects can enter and leave the sensor’s field of view, necessitating track initiation and deletion algorithms. 

Further issues emerge when spurious observations can arise from non-tracked, background objects or when the tracked objects can be temporarily occluded. 

In such cases, the assignment space for matching tracks to observations should be expanded to include these possibilities in order to achieve best performance.


##### 가. Nearest Neighbour

The Nearest Neighbour (NN) approach is perhaps the simplest assignment method for performing data association.

1. one first calculates a distance matrix $$D \in R^{N×N}$$ between every track and every observation

2. Then, one greedily matches detections to tracks by sequentially selecting the closest, unassigned track-detection pair from D until all are assigned.

Several metrics exists for the track-observation distance calculation
- Euclidian distance
- Mahalanobis distance

장/단점 `The NN data association approach benefits from a simple implementation, however,due to its greedy assignment method, it is suboptimal`

##### 나. Global Nearest Neighbour


The Global Nearest Neighbour (GNN) approach is a data association method which 
- minimizes the cumulative distance of all assignments in the matrix D. 

This typically results in less assignment errors compared to the NN approach

In the literature, finding the matchings in D which minimize the cumulative distance is typically referred to as the 
- linear assignment problem 
- simply the assignment problem [14]

There exist a number of published methods and libraries for finding the optimal solution. For example, two commonly used methods are 
- the Munkres assignment algorithm [40] and 
- the Jonker-Volgenant assignment algorithm [33].

While the GNN approach is typically superior to the NN approach at producing accurate assignments, it suffers from a slower computation time

##### 다. Other Data Association Approaches

- Probabilistic Data Association Filter
- the MultiHypothesis Tracker  


For more in-depth analyses in this area, the reader is encourged examine existing seminal work [4].

```
[4] Yaakov Bar-Shalom and Xiao-Rong Li. Multitarget-multisensor tracking: principles and techniques, volume 19. Yaakov Bar-Shalom, 1995.
```

##### 라. Track Initiation and Deletion



## 3. Joint Leg Tracker

### 3.1 Autonomous Person Detection

### 3.2 Autonomous Tracking of Multiple People

