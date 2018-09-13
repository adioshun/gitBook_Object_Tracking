|논문명 |High-Speed Tracking-by-Detection Without Using Image Information|
| --- | --- |
| 저자\(소속\) | Erik Bochinski, Volker Eiselein and Thomas Sikora \(\) |
| 학회/년도 | IEEE AVSS 2017, [논문](http://elvera.nue.tu-berlin.de/files/1517Bochinski2017.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 |DETRAC dataset, 2,666 FPS(맥북프로)|
| 관련연구||
| 참고 | [홈페이지](https://motchallenge.net/tracker/IOU17) , [blog(중국어)](https://blog.csdn.net/zhangjunhit/article/details/78911287), [blog(영어)](https://lab.moovel.com/blog/tracking-things-in-object-detection-videos#3b-iou-tracker)|
| 코드 | [깃허브](https://github.com/bochinski/iou-tracker/) |



# IOT Tracker

## 1. Introduction

최근 추적 기법 트랜드 : tracking-by-detection 
1. first an object detector is applied to each video frame. 
2. In a second step, a tracker is used to associate these detections to tracks. 

챌린지 
- limited performance of the underlying detector which may produce false positive and missed detections
- MOT
- Paths become ambiguous

기존 연구 결과 `Many methods have been proposed to solve these problems:`
- [1, 2] define a continuous energy function and search for strong local minima using sophisticated
minimization techniques. 
- [6] estimates short tracklets for unambiguous frames and stitches them according to a dynamics-based similarity. 
- Other approaches include using a globally optimal and locally greedy method and integer linear programming [12] and online discriminative appearance learning [3].

```
[1] A. Andriyenko and K. Schindler. Multi-target tracking by continuous energy minimization. In Proceedings of the IEEE Conference on  (CVPR), pages 1265–1272. IEEE, 2011.
[2] A. Andriyenko, K. Schindler, and S. Roth. Discretecontinuous optimization for multi-target tracking. In Proceedings of the IEEE Conference on  (CVPR), pages 1926–1933. IEEE, 2012.
[6] C. Dicle, O. I. Camps, and M. Sznaier. The way they move: Tracking multiple targets with similar appearance. In Proceedings of the IEEE Conference on  (CVPR), pages 2304–2311, 2013.
[12] H. Pirsiavash, D. Ramanan, and C. C. Fowlkes. Globallyoptimal greedy algorithms for tracking a variable number of objects. In Proceedings of the IEEE Conference on n (CVPR), pages 1201–1208. IEEE, 2011.
[3] S.-H. Bae and K.-J. Yoon. Robust online multi-object tracking based on tracklet confidence and online discriminative appearance learning. In Proceedings of the IEEE Conference on CVPR,pages 1218–1225, 2014.
```


본 논문의 기본 아이디어 : in this paper a very simple tracking approach shall be assessed which is based on the idea of a passive detection filter introduced in [8].

```
[8] V. Eiselein, E. Bochinski, and T. Sikora. Assessing post-detection filters for a generic pedestrian detector in a tracking-by-detection scheme. In Analysis of video and audio ”in the Wild” workshop at IEEE AVSS17, Lecce, Italy, Aug. 2017.
```


## 2. Method

가정사항 
- The detector produces a detection per frame for every object to be tracked, 
    - i.e. there are none or only few ”gaps” in the detections. 
- detections of an object in consecutive frames have an unmistakably high overlap IOU


정의 : We propose a simple IOU tracker 
- which essentially continues a track by associating the detection with the highest IOU to the last detection in the previous frame if a certain threshold σIOU is met. 
- All detections not assigned to an existing track will start a new one. 
- All tracks without an assigned detection will end.

![image](https://user-images.githubusercontent.com/17797922/45467812-61828380-b6d6-11e8-9d45-1c6d246b3a17.png)

- $$D_f$$ denotes the detections at frame $$f$$
- $$d_j$$ the $$j^{th}$$ detection at that frame
- $$T_a$$ active tracks
- $$T_f$$ finished tracks 
- $$F$$ the number of Frames in the sequence

Note that in line 5 only the best-matching, unassigned detection is taken as a candidate to extend the track. 

This does not necessarily lead to an optimal association between the detections Df and tracks $$T_a$$ but could be solved 
- e.g. by applying the Hungarian algorithm maximizing the sum of all IOUs at that frame. 

However, taking the best match is a reasonable heuristic since $$σIOU$$ is normally chosen in the same range as the $$IOU$$ threshold for the non-maxima suppression of the detector. 

Therefore, multiple matches satisfying $$σIOU$$ are rare in practice.

## 3. Experiments

## 4. Conclusions

Our presented IOU tracker considerably outperforms the state-of-the-art at only a fraction of the complexity and computational cost. 

This becomes possible due to the recent advances in the object detection
domain, not at least due to the current boom of CNN-based approaches. 


---

[Tracking Things in Object Detection Videos](https://lab.moovel.com/blog/tracking-things-in-object-detection-videos#3b-iou-tracker)의 정리글 

### 동작 방식 

It's incredibly simple, it works by comparing the overlapping areas between the two detections between the frames.

![](https://lab.moovel.com/content/3-blog/1-tracking-things-in-object-detection-videos/iou-tracker.png)

It does this by computing the intersection over union or the areas: $$ IOU(a,b) = \frac{Area(a) \cap Area(b)}{Area(a) \cup Area(b)} $$

And it does just that (no prediction, no velocity vector computation...)


### 제약 Limitations

- 예측을 하지 않아 특정 프레임에서 탐지를 하지 못한다면, 다음 프레임에서 새로운 ID를 할당 `Doesn't do any prediction, so if YOLO loses the object for some frames, the tracker will lose it as well and will track it again under a new id.`

- Won't perform well on lower frame rate detections, this is understandable, the overlapping areas at lower frame rates can be non existent as there is no predictions.


### How does it perform on our use case of tracking cars ?

- Surprisingly great ! 

- We think out of the box it may not be as good as our current algorithm tracker for some case because YOLO is missing detections quite a lot of times and triggers lots of re-assignments with this tracker... 

- but it had a huge potential of improvement if we add prediction + re-entering features.


### Takeaways from the IOU tracker

> SIMPLE IS THE BEST : “simple tracking methods like the IOU tracker can lead to better results than complex approaches based on decades of research”

기존 유클리드 기반 distance()함수를 IOU로 바꾸면 성능 향상 가능 `Based on what we learned we revisited our `distance()` function. It could be improved by using this overlapping area comparison.`




















