|논문명 |Detect to Track and Track to Detect|
| --- | --- |
| 저자\(소속\) | \(\) |
| 학회/년도 | ICCV 2017, [논문](https://arxiv.org/abs/1710.03958) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 | |
| 관련연구||
| 참고 | [홈페이지](http://www.robots.ox.ac.uk/~vgg/research/detect-track/), [Youtube](https://www.youtube.com/watch?v=m9GarFWuVwk) |
| 코드 | [깃허브](https://github.com/feichtenhofer/Detect-Track) |


# Detect to Track and Track to Detect



## 1. Introduction


기존의 `tracking by detection` 방식은 새로운 패러다임이지만 frame-level detection 방식을 장악 하진 못하였다.

```
In the case of object detection and tracking in videos,

recent approaches have mostly used detection as a first step, followed by post-processing methods such as applying a tracker to propagate detection scores over time.

Such variations on the ‘tracking by detection’ paradigm have seen impressive progress but are dominated by frame-level detection methods
```

### ImageNet video object detection challenge (VID)와 ImageNet object detection (DET) challenge 차이

1. (i) size: the sheer number of frames that video provides (VID has around 1.3M images, compared to around 400K in DET or 100K in COCO [22]),
2. (ii) motion blur: due to rapid camera or object motion,
3. (iii) quality: internet video clips are typically of lower quality than static photos,
4. (iv) partial occlusion: due to change in objects/viewer positioning, and
5. (v) pose: unconventional object-to-camera poses are frequently seen in video

이러한 문제점을 해결 하기 위해서 VID에서 좋은 성적을 보이는 알고리즘은 frame-level detectors 이전에 **exhaustive post-processing** 을 수행 한다.
- For example,: the winner [17] of ILSVRC’15 uses two multi-stage Faster R-CNN [31] detection frameworks, context suppression, multi-scale training/testing, a ConvNet tracker [39], optical-flow based score propagation and model ensembles.
