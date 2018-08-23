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




![](https://i.imgur.com/5hbE0Mo.png)





![](https://i.imgur.com/iAcbBz6.png)