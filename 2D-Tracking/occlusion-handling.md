# [Multiple Object Tracking: A Literature Review](https://arxiv.org/abs/1409.7618)


### 3.5 Occlusion Handling

맞물림은 MOT에서 가장 큰 문제이다. `Occlusion is perhaps the most critical challenge in MOT. `

맞물림으로 인해 ID변경이나 궤도 단절이 발생 한다. `It is a primary cause for ID switches or fragmentation of trajectories. `

In order to handle occlusion, various kinds of strategies have been proposed.

#### 3.5.1 Part-to-whol

#### 3.5.2 Hypothesize-and-tes

#### 3.5.3 Buffer-and-recove

#### 3.5.4 Others

---

# [LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf)

> 2012, 석사 학위 논문

### 2.5 Approaches for occlusion\(맞물림\) handling

사람이 많은 곳에서 서로 가려짐이 발생할경우 추적이 어렵게 된다.

The temporary occlusion of the objects may lead to mismatch when they return to view.

To maintain estimates of the tracks during occlusion, it is critical to have an estimate of the motion model of the objects during occlusion \[64\].

```
[64] R. Rosales and S. Sclaroff, “Improved tracking of multiple humans with trajectory prediction and occlusion modeling,” IEEE CVPR Workshop on the Interpretation of Visual Motion,1998
```

해결 방법 : 이전장에 언급한 filltering알고리즘에 기능을 추가 하여 해결 가능 `To some extent, this occlusion problem can be resolved using some of the previously-mentioned filtering methods necessary in laser-based tracking systems.`

* 움직임 예측 가능 : 칼만 필터
* 움직임 예측이 불가능 함\(칼만필터기반\) : IMM\(Interactive Multiple Model\), 일반적으로 사용됨
* runs several Kalman Filters with different models parallel and merge the outputs to predict the positions \[22, 28, 42, 52\].
* 움직임 예측이 불가능 함\(확률 기반\) : 파티클 필터
* probability based model in a particle filter can deal with complex dynamic motion

#### A.Explicit model with Kalman Filter

#### B. Probability model with particle filter

#### C. Interacting Multiple Models \(IMM\)

#### D. Dynamic Model