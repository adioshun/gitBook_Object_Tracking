### [A Review of Object Detection and Tracking Methods](http://www.ijaerd.com/papers/finished_papers/A Review of Object Detection and Tracking Methods-IJAERDV04I1045913.pdf):2017

Object Tracking: A Survey

http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.112.8588&rep=rep1&type=pdf

# Object Tracking

![](https://i.imgur.com/XTcifmI.png)

## 1. Detection 

### 1.1 Manual하게 사람이 지정 

- 마우스 Drag를 통해 대상 지정

### 1.2 Automatic하게 시스템이 탐지 



## 2. Modeling 

- 추적 물체를 구분하기 위한 표현 방법들 




### 2.1 Object Representation 

![](https://i.imgur.com/d98tMDv.png)


### 2.2 Appearace Feature (Descriptor)

## 3. Tracing Algorithm

> 추적 알고리즘은 object representation에 따라 달라 질수 있다. 

![image](https://user-images.githubusercontent.com/17797922/40040689-303d1cce-5856-11e8-86c5-07293af6f9ec.png)



### 3.1 Feature based

- Color feature : Histogram, Meanshfift
- Interest point operator : Local feature, SIFT, SURF, HOG
- Texture : Gabor wavelet, LBP
- Optical Flow

### 3.2 Estimation(=filtering) based 

> Tracking을 일종의 state estimation으로 간주 

- Kalman filter, extended KF, unscented KF
- Particle filter

### 3.3 Segmentation based

- Background subtraction 

### 3.4 Appearance based

- kernal based
- patch based 

### 3.5 Learning based

- SVM
- NN
- Bosting


---

The tasks of detecting the object and establishing correspondence between the object instances across frames can either be performed **separately** or **jointly**. 

In the first case, 
- possible object regions in every frame are obtained by means of an object detection algorithm, 
- and then the **tracker** corresponds objects across frames. 

In the latter case, 
- the object region and correspondence is jointly estimated by iteratively updating object location and region
information obtained from previous frames. 

In either tracking approach, 
- the objects are represented using the shape and/or appearance models described in Section 2. 
- The model selected to represent object shape limits the type of motion or deformation it can undergo. 
    - For example, if an object is represented as a point, then only a translational model can be used. 
    - In the case where a geometric shape representation is used for the object, parametric motion models like affine or projective transformations are appropriate. 




![](https://i.imgur.com/udmzbwR.png)

#### Point Tracking. 

- Objects detected in consecutive frames are represented by points, 

- and the association of the points is based on the previous object state which can include object position and motion. 

- This approach requires an external mechanism to detect the objects in every frame. 

> An example of object correspondence is shown in Figure 8(a).

#### Kernel Tracking. 

> Kernel refers to the object shape and appearance. (eg.: rectangular template or an elliptical shape with an associated histogram. )

- Objects are tracked by computing the **motion of the kernel** in consecutive frames (Figure 8(b)). 

- This motion is usually in the form of a parametric transformation such as translation, rotation, and affine.

#### Silhouette Tracking. 

- Tracking is performed by **estimating the object region** in each frame. 

- Silhouette tracking methods use the information encoded inside the object region. 

- This information can be in the form of appearance density and shape models which are usually in the form of edge maps. 

- Given the object models, silhouettes are tracked by either **shape matching** or **contour evolution** (see Figure 8(c), (d)). 

- Both of these methods can essentially be considered as object segmentation applied in the temporal domain using the priors generated from the previous frames.


![](https://i.imgur.com/5hbE0Mo.png)

## 1. Point Tracking

- Tracking can be formulated as the correspondence of detected objects represented by points across frames. 

- Overall, point correspondence methods can be divided into two broad categories, 
    - Deterministic methods : use qualitative motion heuristics to constrain the correspondence problem. 
    - Statistical methods : take the object measurement and take uncertainties into account to establish correspondence.

### 1.1 Deterministic Methods for Correspondence. 

- Deterministic methods for point correspondence define a cost of associating each object in frame t − 1 to a single object in frame t using a set of motion constraints. 

- Minimization of the correspondence cost is formulated as a combinatorial optimization problem. 

- A solution, which consists of one-to-one correspondences (Figure 9(b)) among all possible associations (Figure 9(a)), can be obtained by optimal assignment methods, for example, Hungarian algorithm, [Kuhn 1955] or greedy search methods. 

- The correspondence cost is usually defined by using a combination of the following constraints.
    - Proximity assumes the location of the object would not change notably from one frame to other (see Figure 10(a)).
    - Maximum velocity defines an upper bound on the object velocity and limits the possible correspondences to the circular neighborhood around the object (see Figure 10(b)).
    - Small velocity change (smooth motion) assumes the direction and speed of the object does not change drastically (see Figure 10(c)).
    - Common motion constrains the velocity of objects in a small neighborhood to be similar (see Figure 10(d)). This constraint is suitable for objects represented by multiple points.
    - Rigidity assumes that objects in the 3D world are rigid, therefore, the distance between any two points on the actual object will remain unchanged (see Figure 10(e)).
    - Proximal uniformity is a combination of the proximity and the small, velocity change constraints.


### 1.2 Statistical Methods for Correspondence. 

- Statistical correspondence methods solve these tracking problems by taking the measurement and the model uncertainties into account during object state estimation. 
    - Measurements obtained from video sensors invariably contain noise. 
    - Moreover, the object motions can undergo random perturbations, for instance, maneuvering vehicles. 

- The statistical correspondence methods use the state space approach to model the object properties such as position, velocity, and acceleration.

- Measurements usually consist of the object position in the image, which is obtained by a detection mechanism. 

- Followings, we will discuss the state estimation methods in the context of point tracking, however, it should be noted that these methods can be used in general to estimate the state of any time varying system. 

- For example, these methods have extensively been used for tracking contours, activity recognition, object identification, and structure from motion ].


#### A.  Single Object State Estimation

##### 가. 칼만필터 

##### 나. Particle Filters

#### B. Multiobject Data Association and State Estimation

- When tracking multiple objects using Kalman or particle filters, one needs to deterministically associate the most likely measurement for a particular object to that object’s state, that is, the correspondence problem needs to be solved before these filters can be applied. 

- The simplest method to perform correspondence is to use the nearest neighbor approach. 

- However, if the objects are close to each other, then there is always a chance that the correspondence is incorrect. 

- An incorrectly associated measurement can cause the filter to fail to converge. 

- There exist several statistical data association techniques to tackle this problem.

##### 가. Joint Probability Data Association Filter

##### 나. Multiple Hypothesis Tracking (MHT )

---

![](https://i.imgur.com/iAcbBz6.png)