# [Tracking Things in Object Detection Videos](https://lab.moovel.com/blog/tracking-things-in-object-detection-videos)

> [깃허브](https://github.com/tdurand/node-moving-things-tracker)

## 1. Our problem

YOLO는 물체는 탐지 하지만 ID를 부여 하지 못함 

## 2. First “intuitive” algorithm

```cpp

currentlyTrackedObjects = []
For each frame:
  // 1. Try to match the currently tracked object with the detections of this frame
  For each detections:
    doesMatchExistingTrackedObject(detection, currentlyTrackedObjects)
    // if it matches, update the trackedObject position
    matchedTrackedObject.update(detection)
  // 2. Assign unmatched detections to new objects
  currentlyTrackedObjects.add(new trackedObject(detection))
  // 3. Clean up unmatched tracked objects
  For each currentlyTrackedObjects:
    if isUnmatched(trackedObject):
      trackedObject.remove()
      
```

`doesMatchExistingTrackedObject()`function :compare two detections, how to determine if they are tracking the same object ?

-  `distance() function`: 두 탐지 대상의 위치를 비교하여 상대 거리를 계산 한다. `which compare two detections positions (current detections and candidate for next frame) and determine their relative distance. `
  - 충분히 가까운 거리이며 같은 물체로 판별 한다. `If they are considered close enough, we can match them.`


```cpp
function distance(item1, item2) {
  // compute euclidian distance between centers
  euclidianDistance = computeEuclidianDistance(item1, item2)
  if (euclidianDistance > DISTANCE_LIMIT):  
    // Do not match
  else:
    // Potential match
}
```

- 성능 및 제약 : This early implementation was already pretty good and matching correctly ~80% of the detections, but still had lots of re-assignments 
  - (when we lose track of the object and we assign it a new id even if it is the same object).

    
- 해결방안 : At that point we had some ideas on how to improve it:
  1. By keeping a memory of the unmatched item for a few frames and avoid removing them directly 
    - (sometimes the detection algorithms miss the object for a few frames)
  2. By predicting the position on the new frame with a velocity vector
  3. By improving this distance function
  

### 2.1 Keep unmatched object in memory


바로 삭제 하는것이 아니라, 몇 프레임정도 기다렸다가 삭제 한다. `We first integrated the idea of keeping in memory the unmatched items for a few frames which is simply wait a few frames before removing it from the tracked items.`

```cpp

if isUnmatched(trackedObject):
    trackedObject.unmatchedThisFrame()

## unmatchedThisFrame() 함수 
function unmatchedThisFrame() {
  nbUnmatchedFrame++
  if nbUnmatchedFrames > 5:
    //Effectively delete the item
    this.remove()
}

```

이 방식을 통해 놓친 대상에 대한 회복 및 ID 재할당을 방지 한다. `This made the tracker more resilient to missing detections from YOLO and avoided some reassignments,`
- 그러나 효율적 적용을 위해서는 다음 위치를 예측 할수 있어야 한다. `but in order to have it more effective, we needed also to predict the next position.`

### 2.2 Predict position by computing the velocity vector

The idea behind this to be able to predict the next position of the tracked object if it is missing in the next frame, so it moves to its “theorical” position and will be more likely to be re-matched on the next frame.

```cpp

if isUnmatched(trackedObject):
   trackedObject.predictNextPosition()
   trackedObject.unmatchedThisFrame()
And the predictNextPosition() function looks like this

function predictNextPosition() {
  x: trackedObject.x + velocityVector.dx,
  y: trackedObject.y + velocityVector.dy
}

```

### 2.3 Improving the distance function

현 시점에서는 개선 방법이 떠오르지 않음 CV 연구를 통해 도출 예정 `At this point we didn’t have much clue on how to improve it, we felt the need to review some computer vision literature about tracking to make sure we were not missing some good ideas.`


## 3. Literature review


We found some useful papers for our problem statement. Check them out here:

- [High-Speed Tracking-by-Detection Without Using Image Information (Bochinski, Eiselein and Sikora) ](http://elvera.nue.tu-berlin.de/files/1517Bochinski2017.pdf)

- [Simple Online and Realtime Tracking (Bewley, Zongyuan Ge, Ott, Ramos, Upcroft)](http://arxiv.org/abs/1602.00763)

- [OpenCV Matching Faces Over Time (Dan Shiffman)](http://shiffman.net/general/2011/04/26/opencv-matching-faces-over-time/)


### 3.1 General things about tracking

We've identified two types of tracking:
- 단일 물체 추적(single object tracking): you choose one thing on the video and track it across all the frames
- 다중 물체 추적(multiple object tracking,MOT): track multiple object across all frames


And for each of them, there is two possibilities:
- 비실실간(Not real time tracking): algorithms that run on an existing video slower than real time 
  - (ie, takes more than a frame time to compute the next state of the tracker)
- 실시간(Real time tracking): the tracking algorithms that can run in real time 
  - (necessary for self-driving cars, robot ... )


We noticed that 
- 실시간 알고리즘은 the real time algorithms use only the **detections inputs** (done by YOLO for ex), 
- 비실시간 알고리즘은 the non real time trackers use information from the **image frames** to get more data to do the tracking. 

> 대부분의 연구는 단일 물체 추적에 초점을 두고 있음 `Also most of the papers and projects published are focusing on single object tracking and not MOT`


Historically there was almost no algorithm working only on the detections output only as the detections weren't as good / fast as the recent progress of neural network based detector such as YOLO, and they needed to get more data from the image frame to do their job. But now this is changing and the tracking algorithms get simpler and faster as the detections are better. This technique is also called doing **tracking by detections**.

> “Due to recent progress in object detection, tracking-by-detection has become the leading paradigm in multiple object tracking.” [[출처:SORT deep paper]](https://arxiv.org/pdf/1703.07402.pdf)

본 문서에서는 tracking-by-detection기법을 적용하지 않았다. `That said there are maybe tracking approaches using image data that lead to better tracking results than just "tracking by detections" , but we haven’t looked into them as they will be more complex to run and may likely not run in real time: for example color based tracking, particle tracking ...`

### 3.2 Our problem set


> 주요 내용 없음 


### 3.3 Benchmarking existing solutions
  

[MOT 추적 벤치마킹](https://motchallenge.net/)
 : A challenge exists for researcher to compare their tracking algorithm, and it is specifically designed for Multiple object tracking: 

많은 알고리즘 중에 하기 두가지 특징을 가지는 알고리즘을 분석 대상으로 삼았다. `There are plenty of algorithm, but we benchmarked two of them that had the following criterias:`
- run at more the 25 FPS
- open source implementation done in Python / C++


#### A. SORT : Simple Online and Realtime Tracking

https://adioshun.gitbooks.io/object-tracking/content/2dtracking/2016-sort-simpleonlinerealtimetracking.html



#### B. IOU Tracker:



https://adioshun.gitbooks.io/object-tracking/content/2dtracking/2017-iou-tracker.md















  