|논문명 |High-Speed Tracking-by-Detection Without Using Image Information|
| --- | --- |
| 저자\(소속\) | Erik Bochinski, Volker Eiselein and Thomas Sikora \(\) |
| 학회/년도 | IEEE AVSS 2017, [논문](http://elvera.nue.tu-berlin.de/files/1517Bochinski2017.pdf) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 |2,666 FPS(맥북프로)|
| 관련연구||
| 참고 | [홈페이지](https://motchallenge.net/tracker/IOU17) , [blog(중국어)](https://blog.csdn.net/zhangjunhit/article/details/78911287), [blog(영어)](https://lab.moovel.com/blog/tracking-things-in-object-detection-videos#3b-iou-tracker)|
| 코드 | [깃허브](https://github.com/bochinski/iou-tracker/) |


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

