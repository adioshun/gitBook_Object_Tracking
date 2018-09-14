|논문명 |Fast and Furious: Real Time End-to-End 3D Detection, Tracking and Motion Forecasting with a Single Convolutional Net |
| --- | --- |
| 저자\(소속\) | Wenjie Luo\(우버\) |
| 학회/년도 | CVPR 2018, [논문](http://openaccess.thecvf.com/content_cvpr_2018/papers/Luo_Fast_and_Furious_CVPR_2018_paper.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | [기사](https://www.utoronto.ca/news/autonomous-vehicles-u-t-researchers-make-advances-new-algorithm),  [Youtube_CVPR2018](https://youtu.be/Jl1NeziAHFY?t=27m55s) |
| 코드 ||






이전 연구?
- SBNet: [Sparse Blocks Network for Fast Inference](http://www.cs.toronto.edu/~mren/sbnet/index.html), [[code]](https://eng.uber.com/sbnet/), [[github]](https://github.com/uber/sbnet), [[arxiv]](https://arxiv.org/abs/1801.02108)

관련 연구
- [PIXOR: Real-time 3D Object Detection from Point Clouds](http://openaccess.thecvf.com/content_cvpr_2018/papers/Yang_PIXOR_Real-Time_3D_CVPR_2018_paper.pdf): CVPR2018


# 1. Introduction

자율주행차의 주요 기술 `Modern approaches to self-driving divide the problem into four steps: `
- detection, 
- object tracking, 
- motion forecasting
- and motion planning. 

기존방식은 계측적 카스게이드 방식이었다. `A cascade approach is typically used where the output of the detector is used as input to the tracker, and its output is fed to a motion forecasting algorithm that estimates where traffic participants are going to move in the next few seconds. `

여러 단점이 존재 한다. 


본 논문에서는 BEV방식을 활용하여 네트워크를 설계 하였다. `We take advantage of 3D sensors and design a network that operates on a bird-eye-view (BEV) of the 3D world.`


Our approach is a one-stage detector that takes a 4D tensor created from multiple consecutive temporal frames as input and performs 3D convolutions over space and time to extract accurate 3D bounding boxes. 

Our model produces bounding boxes not only at the current frame but also multiple timestamps into the future. 

We decode the tracklets from these predictions by a simple pooling operation that combine the evidence from past and current predictions.

# 2. Related Work

## 2D Object Detection

R-CNN 계열과 YOLO계열이 있다. 

## 3D Object Detection

The ideas behind modern 2D image detectors can be transferred to 3D object detection. 

Chen et al. [2] used **stereo images** to perform 3D detection. 

```
[2] X. Chen, K. Kundu, Y. Zhu, H. Ma, S. Fidler, and R. Urtasun. 3d object proposals using stereo imagery for accurate object class detection. IEEE Transactions on Pattern Analysis and Machine Intelligence, 2017.
```

Li [15] used 3D point cloud data and proposed to use 3D convolutions on a voxelized representation of point clouds. 


```
[15] B. Li. 3d fully convolutional network for vehicle detection in point cloud. arXiv preprint arXiv:1611.08069, 2016
```

Chen et al. [3] combined image and 3D point clouds with a fusion network. 
    - They exploited 2D convolutions in BEV, 
    - however, they used hand-crafted height features as input.
    - They achieved promising results on KITTI [6] but only ran at 360ms per frame due to heavy feature computation on both 3D point clouds and images. 
    - This is very slow, particularly if we are interested in extending these techniques to handle temporal data.


```
[3] X. Chen, H. Ma, J. Wan, B. Li, and T. Xia. Multi-view 3d object detection network for autonomous driving. arXiv
preprint arXiv:1611.07759, 2016. 
```



## Object Tracking

In this section we briefly review the use of deep learning in tracking. 

Pretrained CNNs were used to extract features and perform tracking with correlation [18] or regression [29, 9]. 

```
[18] C. Ma, J.-B. Huang, X. Yang, and M.-H. Yang. Hierarchical convolutional features for visual tracking. In Proceedings of the IEEE International Conference on Computer Vision, pages 3074–3082, 2015
[29] L. Wang, W. Ouyang, X. Wang, and H. Lu. Visual tracking with fully convolutional networks. In Proceedings of the IEEE International Conference on Computer Vision, pages 3119–3127, 2015
[9] D. Held, S. Thrun, and S. Savarese. Learning to track at 100 fps with deep regression networks. In European Conference on Computer Vision, pages 749–765. Springer, 2016
```

Wang and Yeung [30] used an autoencoder to learn a good feature representation that helps tracking. 

```
[30] N. Wang and D.-Y. Yeung. Learning a deep compact image representation for visual tracking. In Advances in neural information processing systems, pages 809–817, 2013
```

Tao et al. [27] used siamese matching networks to perform tracking. 

```
[27] R. Tao, E. Gavves, and A. W. Smeulders. Siamese instance search for tracking. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 1420–1429, 2016.
```

Nam and Han [21] finetuned a CNN at inference time to track object within the same video.

```
[21] H. Nam and B. Han. Learning multi-domain convolutional neural networks for visual tracking. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, pages 4293–4302, 2016
```




---

![](https://i.imgur.com/wuNOkP6.png)

Dataset : Uber TOR4D datasets






