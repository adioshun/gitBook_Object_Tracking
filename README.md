# Summary

## Tracking

* [Introduction](README.md)
* [Tracking 개요](tracking.md)
* [칼만필터](https://legacy.gitbook.com/book/adioshun/kalmanfilter/details)



## 2D Object Tracking

* [2D Background-filter](https://adioshun.gitbooks.io/gitbook_from_github/content/opencvbackgroundsubtractor.html)
* [2D\_Detection](https://adioshun.gitbooks.io/deep_drive/content/)
* [2D\_Tracking](2dtracking.md)
  * [Mean Shift\_CAM shift](2dtracking/mean-shift.md)
  * [2006-Survey-Object-tracking](2dtracking/2006-survey-object-tracking.md)
  * [2012-TLD](2dtracking/pn-tracker.md)
  * [2014-Survey-ObjectDetection-TrackingMethods](2dtracking/2014-survey-objectdetection-trackingmethods.md)
  * [2016- GOTURN](2dtracking/2016-goturn.md)
  * [2016-SORT-SimpleOnlineRealtimeTracking](2dtracking/2016-sort-simpleonlinerealtimetracking.md)
  * [2017-Detect2Track-Track2Detect](2dtracking/2017-detect2track-track2detect.md)
  * [2018-blog-Tracking-things](2dtracking/2018-blog-tracking-things.md)

## 3D Object Tracking

* [3D Background-filter](background-filter.md)
  * [2016-Change-Detection-of-Mobile-lidar-data](background-filter/2016-change-detection-of-mobile-lidar-data.md)
* [3D\_Detection](3ddetection.md)
  * [2018-pixor](3dtracking/2018-pixor.md)
* [3D\_Tracking](3dtracking.md)
  * [2007-SLAMMOT](3dtracking/2007-slammot.md)
  * [2008-Model based vehicle tracking for autonomous driving in urban environments](3dtracking/2008-model based vehicle tracking for autonomousdriving in urban environments.md)
  * [2010-Tracking People with a 360 degreelidar](3dtracking/2010-Tracking-People-with-a-360-degree-lidar.md)
  * [2011-Tracking People in 3D Using a Bottom-Up Top-Down Detector](3dtracking/2011-tracking-people-in-3d-using-a-bottom-up-top-down-detector.md)
  * [2012-Lidar-Based-MOT-system-with-Dyanamic-modeling](3dtracking/2012-lidar-based-mot-system-with-dyanamic-modeling.md)
  * [2014-Confidence-Based-PedestrianTracking](3dtracking/2014-confidence-based-pedestriantracking.md)
  * [2015-PersonTracking-2D-Lidar](3dtracking/2015-persontracking-2d-lidar.md)
  * [2017-Low resolution lidar-based multi-object tracking for driving applications](3dtracking/2017-low-resolution-lidar-based-multi-object-tracking-for-driving-applications.md)
  * [2017-3D-Lidar MOT for Autonomous-Driving](3dtracking/2017-3d-lidar-mot-for-autonomous-driving.md)
  * [2017-online Learning](3dtracking/2017-Online learning for human classification in 3D LiDAR-based tracking.md)
  * [2018-Fast and Furious](3dtracking/2018-fast-and-furious.md)

## Tracker

* [IOU\_Tracker](tracker/ioutracker.md)
* [centroid\_tracker](tracker/centroidtracker.md)
* [2017-IOU-Tracker](2dtracking/2017-iou-tracker.md)
* [근접 노드 찾기](https://github.com/adioshun/gitBook_Object_Tracking/blob/master/tracker/How-to-calculate-distance.ipynb)

## Data Association

* [Data-Association](data-association.md)
  * [2014-Survey-Multi-target Tracking Filters and Data Association](data-association/2014-survey-multi-target-tracking-filters-and-data-association.md)
  * [Terms-Data-Association](data-association/terms-data-association.md)
  * [Multiple Hypothesis Tracking](data-association/multiple-hypothesis-tracking.md)
  * [two-point differencing](data-association/two-point-differencing.md)
  * [GM-PHD filter](data-association/gm-phd-filter.md)

## ID Management

* [Assignment ](assignment.md)
  * [Hungarian-method](hungarian-method.md)



## Condensation

* [Condensation](Condensation.md)
  * [code](Condensation/Condensation-code.md)

## Implementation

* [dlib](implementation/dlib.md)
* [Snippet](implementation/snippet.md)
* [이미지내 사람추적](implementation/surveillance.md)

## 참고

* [Datasets](datasets.md)
  * [2D-Tracking-Datasets](2d-tracking-datasets.md)
* [Application-Counting](application-counting.md)

---

# 추천 자료 

하지만 트래킹에 대한 전반적인 이해를 돕기 위해서 책을 하나 추천 드리면



```
Yaakov Barshalom, X. Rong Li, Estimation with Applications to Tracking and Navigation
```
https://onlinelibrary.wiley.com/doi/book/10.1002/0471221279
http://read.pudn.com/downloads117/ebook/497286/Estimation%20with%20Applications%20to%20Tracking%20and%20Navigation%E6%9D%8E%E6%99%93%E6%A6%95.pdf

입니다. 저는 처음이 책을 접하지 않고 두서없이 공부를 하였지만 제가 추천 드리는 책이 제가 생각하기로는 기본적인 트래킹 알고리즘에 대한 설명이 잘 되어 있는 것으로 생각됩니다. 




그 다음으로는 비선형 시스템의 상태를 추적할 경우 필요한 extended kalman filter, unscented kalman filter, particle filter에 대해 연구하시고 싶으시면 아래 논문과 책을 보시면 도움이 되실거라 생각됩니다.


```
S.J. Julier, and J.K. Uhlmann, “New Extension of the Kalman Filter to Nonlinear Systems,” Proceedings of the SPIE 3068, Signal Processing, Sensor Fusion, and Target Recognition VI, pp. 182-193,1997.
 S.J. Julier, and J.K. Uhlmann, “Unscented Filtering and Nonlinear Estimation,” Proceedings of the IEEE, vol. 92, no. 2, pp. 401-422, 2004.
B. Ristic, S. Arulampalam, N. Gordon, Beyond the Kalman Filter. Artech House:Norwood, MA, USA, 2004.
```



다음으로 data association에 대해 연구하시려면 아래 책과 기본적인 NN, SN, PDA를 위한 논문을 읽어 보시면 많은 도움이 되리라 생각됩니다.

```
Y. Bar-Shalom and T. E. Fortmann, Tracking and data association. New York:Academic, 1988.
X.R. Li, and Y. Bar-Shalom, “Tracking in Clutter with Nearest Neighbor Filters: Analysis and Performance,” IEEE Transactions on Aerospace and Electronic Systems, vol. 32, no. 3, pp. 995-1010, 1996.
X.R. Li, “Tracking in Clutter with Strongest Neighbor Measurements - Part I: Theoretical Analysis,” IEEE Transactions on Automatic Control, vol. 43, no. 11, pp. 1560-1578, 1998.
Y. Bar-Shalom, and E. Tse, “Tracking in a Cluttered Environment with Probabilistic Data Association,” Automatica, pp. 451-460, Sep. 1975.
```


특히 Y. Bar-Shalom이 지은 책 두권은 표적 추적에 관련하여 매우 좋은 책으로 생각됩니다. 최대한 간추리고 기본적인 알고리즘들에 대한 논문과 책을 소개 시켜 드립니다. 소개드린 논문과 책 말고 좀더 심도 있는 연구가 필요하시면 (예를 들어 track management, multi-target tracking algorithm 등)에 관심이 있으시면 연락 주시면 관련 자료들을소개 시켜 드리겠습니다. 

---

# [CVPR 2019 Tracking](https://github.com/shijieS/ComputerVisionSummarization#7-tracking)

- [Multivariate Kalman Filters - Working with Multiple State Variables](https://github.com/shijieS/ComputerVisionSummarization/blob/master/codebook/06-Multivariate-Kalman-Filters.ipynb): 쥬피터

---

# [Deep-Learning-for-Tracking-and-Detection](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/ReadMe.md)


Collection of papers and other resources for object detection and tracking using deep learning

## Object Detection
- **Mask R-CNN** ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Object%20Detection/Mask%20R-CNN%20ax17_4.pdf), [arxiv](https://arxiv.org/abs/1703.06870), [github](https://github.com/CharlesShang/FastMaskRCNN)) by Facebook AI Research!
  * Summary goes here...
- Tensorflow object detection API: https://github.com/tensorflow/models/tree/master/object_detection. Only the two SSD nets can run at 12.5 FPS on one GTX 1080 TI (less accurate than YOLO 604x604). Next two models at 4-5 FPS (4-5% mAP better than YOLO). Best model < 1 FPS. Currently code only allow inference of 1 image at a time. Speed might improve by 2.5 times when they allow multiple image inference.
## Object Tracking
- Multi Object Tracking
	- **Learning to Track: Online Multi-object Tracking by Decision Making** (ICCV 2015) (Stanford) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Learning%20to%20Track%20Online%20Multi-object%20Tracking%20by%20Decision%20Making%20%20iccv15.pdf), [github (Matlab)](https://github.com/yuxng/MDP_Tracking), [project page](https://yuxng.github.io/))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/Learning_to_Track_Online_Multi-object_Tracking_by_Decision_Making__iccv15.pdf)

	- **Tracking The Untrackable: Learning To Track Multiple Cues with Long-Term Dependencies** (arxiv April 2017) (Stanford) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Deep%20Learning/Tracking%20The%20Untrackable%20Learning%20To%20Track%20Multiple%20Cues%20with%20Long-Term%20Dependencies%20ax17_4.pdf), [arxiv](https://arxiv.org/abs/1701.01909), [project page](http://web.stanford.edu/~alahi/))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/Tracking_The_Untrackable_Learning_To_Track_Multiple_Cues_with_Long-Term_Dependencies.pdf)

	- **Near-Online Multi-target Tracking with Aggregated Local Flow Descriptor** (ICCV 2015) (NEC Labs) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Multi%20Target/Near-online%20multi-target%20tracking%20with%20aggregated%20local%20%EF%AC%82ow%20descriptor%20iccv15.pdf), [author page](http://www-personal.umich.edu/~wgchoi/))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/NOMT.pdf)
	  
	- **A Multi-cut Formulation for Joint Segmentation and Tracking of Multiple Objects** (highest MT on MOT2015) (University of Freiburg, Germany) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Batch/A%20Multi-cut%20Formulation%20for%20Joint%20Segmentation%20and%20Tracking%20of%20Multiple%20Objects%20ax16_9%20%5Bbest%20MT%20on%20MOT15%5D.pdf), [arxiv](https://arxiv.org/abs/1607.06317), [author page](https://lmb.informatik.uni-freiburg.de/people/keuper/publications.html))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/A_Multi-cut_Formulation_for_Joint_Segmentation_and_Tracking_of_Multiple_Objects.pdf)
	  
- Single Object Tracking
	- **Deep Reinforcement Learning for Visual Object Tracking in Videos** (arxiv April 2017) (USC-Santa Barbara, Samsung Research) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/RL/Deep%20Reinforcement%20Learning%20for%20Visual%20Object%20Tracking%20in%20Videos%20ax17_4.pdf), [arxiv](https://arxiv.org/abs/1701.08936), [author page](http://www.cs.ucsb.edu/~dazhang/))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/Deep_Reinforcement_Learning_for_Visual_Object_Tracking_in_Videos.pdf)
	  
	- **Visual Tracking by Reinforced Decision Making** (arxiv February 2017) (Seoul National University, Chung-Ang University) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/RL/Visual%20Tracking%20by%20Reinforced%20Decision%20Making%20ax17_2.pdf), [arxiv](https://arxiv.org/abs/1702.06291), [author page](http://cau.ac.kr/~jskwon/))
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/Visual_Tracking_by_Reinforced_Decision_Making_ax17.pdf)

	- **Action-Decision Networks for Visual Tracking with Deep Reinforcement Learning** (CVPR 2017) (Seoul National University) ([pdf](https://drive.google.com/open?id=0B34VXh5mZ22cZUs2Umc1cjlBMFU), [project page](https://sites.google.com/view/cvpr2017-adnet)) 
	  * [Summary](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/Summary/Action-Decision_Networks_for_Visual_Tracking_with_Deep_Reinforcement_Learning_cvpr17.pdf)

	- **End-to-end Active Object Tracking via Reinforcement Learning** (arxiv 30 May 2017) (Peking University, Tencent AI Lab) ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Tracking/RL/End-to-end%20Active%20Object%20Tracking%20via%20Reinforcement%20Learning%20ax17_5.pdf), [arxiv](https://arxiv.org/abs/1705.10561)

## Other potentially useful papers
- **Deep Feature Flow for Video Recognition** ([pdf](https://github.com/abhineet123/Deep-Learning-for-Tracking-and-Detection/blob/master/Object%20Detection/Kaiming%20He%2C%20Mask%20R-CNN%2C%202017.pdf), [arxiv](https://arxiv.org/abs/1611.07715), [github](https://github.com/msracver/Deep-Feature-Flow)) by Microsoft Research
  * Summary goes here...

## Datasets
- [IDOT dataset](https://www.cs.uic.edu/Bits/YanziJin)
- [UA-DETRAC Benchmark Suite](http://detrac-db.rit.albany.edu/)
- [GRAM Road-Traffic Monitoring](http://agamenon.tsc.uah.es/Personales/rlopez/data/rtm/)
- [Stanford Drone Dataset](http://cvgl.stanford.edu/projects/uav_data/)
- [Ko-PER Intersection Dataset](http://www.uni-ulm.de/in/mrm/forschung/datensaetze.html)
- [TRANCOS Dataset](http://agamenon.tsc.uah.es/Personales/rlopez/data/trancos/)
- [Urban Tracker Dataset](https://www.jpjodoin.com/urbantracker/dataset.html)
- [DARPA VIVID / PETS 2005 dataset](http://vision.cse.psu.edu/data/vividEval/datasets/datasets.html) (Non stationary camera)
- [KIT-AKS Dataset](http://i21www.ira.uka.de/image_sequences/) (No ground truth)
- [CBCL StreetScenes Challenge Framework](http://cbcl.mit.edu/software-datasets/streetscenes/) (No top down viewpoint)
- [MOT 2015](https://motchallenge.net/data/2D_MOT_2015/) (mostly street level camera viewpoint)
- [MOT 2016](https://motchallenge.net/data/MOT16/) (mostly street level camera viewpoint)
- [MOT 2017](https://motchallenge.net/data/MOT17/) (mostly street level camera viewpoint)
- [PETS 2009](http://www.cvg.reading.ac.uk/PETS2009/a.html) (No vehicles)
- [PETS 2017](https://motchallenge.net/data/PETS2017/) (Low density; mostly pedestrians)
- [KITTI Tracking Dataset](http://www.cvlibs.net/datasets/kitti/eval_tracking.php) (No top down viewpoint; non stationary camera)

## Resources
- [List of traffic surveillance datasets](https://github.com/gustavovelascoh/traffic-surveillance-dataset) 
- [List of deep learning based tracking papers](https://github.com/handong1587/handong1587.github.io/blob/master/_posts/deep_learning/2015-10-09-tracking.md)
- [List of multi object tracking papers](http://perception.yale.edu/Brian/refGuides/MOT.html)
- [List of single object trackers with results on OTB](https://github.com/foolwood/benchmark_results)
- [List of Matlab frameworks, libraries and software](https://github.com/uhub/awesome-matlab)

## Tutorials
- [Deep Reinforcement Learning: Pong from Pixels](http://karpathy.github.io/2016/05/31/rl/)
- [Demystifying Deep Reinforcement Learning](https://www.intelnervana.com/demystifying-deep-reinforcement-learning/)

## Code
- Multi Object Tracking
	- [Combined Image- and World-Space Tracking in Traffic Scenes (ICRA 2017)](https://github.com/aljosaosep/ciwt)[C++]
	- [Learning to Track: Online Multi-Object Tracking by Decision Making (ICCV 2015)](https://github.com/yuxng/MDP_Tracking)[MATLAB]
	- [Multiple Hypothesis Tracking Revisited (ICCV 2015)](http://rehg.org/mht/) (highest MT on MOT2015 among open source trackers)[MATLAB]
	- [Joint Tracking and Segmentation of Multiple Targets (CVPR 2015)](https://bitbucket.org/amilan/segtracking)[MATLAB]
	- [High-Speed Tracking-by-Detection Without Using Image Information (AVSS 2017)](https://github.com/bochinski/iou-tracker)[Python]
	- [Continuous Energy Minimization for Multitarget Tracking (TPAMI  2014 / CVPR 2011 / ICCV 2011)](https://bitbucket.org/amilan/contracking)[MATLAB]
- Single Object Tracking
	- [Detect to Track and Track to Detect (ICCV 2017)](https://github.com/feichtenhofer/Detect-Track)[MATLAB]
	- [DeepTracking: Seeing Beyond Seeing Using Recurrent Neural Networks (AAAI 2016)](https://github.com/pondruska/DeepTracking)[Torch 7]
	- [Hierarchical Convolutional Features for Visual Tracking (ICCV 2015)](https://github.com/jbhuang0604/CF2)[Matlab]
	- [Learning Multi-Domain Convolutional Neural Networks for Visual Tracking (Winner of The VOT2015 Challenge)](https://github.com/HyeonseobNam/MDNet)[Matlab/MatConvNet]
	- [RATM: Recurrent Attentive Tracking Model](https://github.com/saebrahimi/RATM)[Python]
	- [Visual Tracking with Fully Convolutional Networks (ICCV 2015)](https://github.com/scott89/FCNT)[Matlab]
	- [Fully-Convolutional Siamese Networks for Object Tracking](https://github.com/torrvision/siamfc-tf)[Tensor flow]
	- [ROLO : Spatially Supervised Recurrent Convolutional Neural Networks for Visual Object Tracking](https://github.com/Guanghan/ROLO)[Tensor flow]
	- [Beyond Correlation Filters: Learning Continuous Convolution Operators for Visual Tracking (ECCV 2016)](https://github.com/martin-danelljan/Continuous-ConvOp)[MATLAB]
	- [ECO: Efficient Convolution Operators for Tracking (CVPR 2017)](https://github.com/martin-danelljan/ECO)[MATLAB]
	- [End-to-end representation learning for Correlation Filter based tracking (CVPR 21017)](https://github.com/bertinetto/cfnet)[MATLAB]
	- [A collection of common tracking algorithms](https://github.com/zenhacker/TrackingAlgoCollection)
- Static Object Detection and Matching
	- [Matchnet](https://github.com/hanxf/matchnet)
	- [Stereo Matching by Training a Convolutional Neural Network to Compare Image Patches](https://github.com/jzbontar/mc-cnn)
	- [Asynchronous Methods for Deep Reinforcement Learning ](https://github.com/miyosuda/async_deep_reinforce)
	- [YOLO9000: Better, Faster, Stronger - Real-Time Object Detection. 9000 classes!](https://github.com/philipperemy/yolo-9000)
	- [Deformable Convolutional Networks](https://github.com/msracver/Deformable-ConvNets)
	- [R-FCN: Object Detection via Region-based Fully Convolutional Networks](https://github.com/daijifeng001/R-FCN)
	- [PVANet: Lightweight Deep Neural Networks for Real-time Object Detection](https://github.com/sanghoon/pva-faster-rcnn)
	- [Mask RCNN in TensorFlow](https://github.com/CharlesShang/FastMaskRCNN)
- Video Object Detection
	- [TPN: Tubelet Proposal Network (CVPR 2017)](https://github.com/myfavouritekk/TPN)[Python]
	- [T-CNN: Tubelets with Convolution Neural Networks (CVPR 2016)](https://github.com/myfavouritekk/T-CNN)[Python]
	- [Flow-Guided Feature Aggregation for Video Object Detection (NIPS 2016 / ICCV 2017)](https://github.com/msracver/Flow-Guided-Feature-Aggregation)[Python/CUDA]
- Optical Flow
	- [Fast Optical Flow using Dense Inverse Search (DIS)](https://github.com/tikroeger/OF_DIS)
	- [FlowNet 2.0: Evolution of Optical Flow Estimation with Deep Networks ](https://github.com/lmb-freiburg/flownet2)
- Misc
	- [Darknet: Convolutional Neural Networks](https://github.com/pjreddie/darknet)
	- [RNNexp](https://github.com/asheshjain399/RNNexp)

	


