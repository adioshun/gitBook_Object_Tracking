|논문명 |Simple online and realtime tracking|
| --- | --- |
| 저자\(소속\) | Bewley, Alex and Ge, Zongyuan and Ott, Lionel and Ramos, Fabio and Upcroft, Ben \(\) |
| 학회/년도 | 2016, [논문](https://arxiv.org/abs/1602.00763) |
| Citation ID / 키워드 | |
| 데이터셋(센서)/모델 |25 FPS(맥북 프로) |
| 관련연구||
| 참고 | [홈페이지](https://motchallenge.net/tracker/SORT), [Youtube](https://motchallenge.net/movies/ETH-Linthescher-SORT.mp4) |
| 코드 | [python/C++](https://github.com/abewley/sort), [Tracking-with-darkflow](https://github.com/bendidi/Tracking-with-darkflow) |


|년도|1st 저자|논문명|코드|
|-|-|-|-|
|2016|Alex Bewley|[Simple Online and Realtime Tracking](https://arxiv.org/abs/1602.00763)|[깃허브](https://github.com/abewley/sort)|
|2017|Wojke|Simple Online and Realtime Tracking with a Deep Association Metric|[깃허브](https://github.com/nwojke/deep_sort)|
|2018|Wojke|Deep Cosine Metric Learning for Person Re-identification|-|


---

[Tracking Things in Object Detection Videos](https://lab.moovel.com/blog/tracking-things-in-object-detection-videos#3a-sort--simple-online-and-realtime-tracking)의 정리글 


### 동작 방식 How does it work ?

기본 동작 : it compares a frame with the next using dimensions like position of the bbox, size of the bbox and compute a velocity vector. 


It does have novelties compared to our approach:

- It uses Kalman filters to compute the velocity factor: 
    - Kalman filter is essentially doing some math to smooth the velocity/direction computation by comparing the predicted state and the real detection given by YOLO. 
    - (and I think it smooth out also the size of the bounding box of the predictions)


- Its uses an assignment cost matrix 
    - that is computed as the intersection-over-union (IOU) distance between each detection and all predicted bounding boxes from the existing targets (which is putting all the dimensions in a normalized matrix). 
    - Then the best match is computed using the Hungarian Algorithm, which is a way to fastly compute lots of matrices …


- It also handles the score of the detections (how confident YOLO is of that detection). 
    - the tracker could choose between two close detections based on that.


### 제약 Limitations

Does not handle re-entering: 
- that means that if the tracker loose track of something, when the tracker gets the object back, it will give it a new id, which is bad for us as for the game it means that the masking is lost…
    - The velocity computation is not based on several frames: We've found out that with our algorithm it was better to compute velocity model based on the average of few frames back


### How does it perform on our use case of tracking cars ?

Out of the box not that great. The main problem being that there is high number of identity switches (as it does not handle re-entering). But it does perform better for some cases where our tracker is losing tracking.

Also, and this is true for all trackers of the MOT benchmark, the are optimized for persons, not cars, we didn't try with persons as we didn't shoot footage of persons yet, but we can hope that it performs way better than our algorithm for this.





