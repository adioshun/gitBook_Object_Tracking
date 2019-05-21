### 2.1 Introduction to SOT in clutter

> false detections = clutter.

#### 2.1.1 Introduction to SOT in clutter

- SOT in clutter is a special case of MOT 

- 하나의 물체만 존재 

- This makes single object tracking more similar to **Kalman filtering** and the type of **nonlinear
filtering** problems 

- challenges 
    - Time varying state variables
    - Noisy measurement 
    - missed detection 
    - clutter detection (잡음)
    - Unknown data associations 
    



---

#### 2.2.1 Single object motion and measurement models

> Bernoulli distribution is central to both SOT and MOT (탐지 = 0, 미탐지 = 1)

##### 가. Single Object Motion Models 


> SOT의 Motion model 표기시 $$\pi_k $$ 사용  

![](https://i.imgur.com/XUDlYtc.png)
