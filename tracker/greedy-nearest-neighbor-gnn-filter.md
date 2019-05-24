# [LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf): 2012, 석사 학위 논문

간단하면서도 많이 쓰이는 방법은 GNN이다. `The simplest and probably the most widely applied data association approach is the Greedy Nearest Neighbor Filter.`

The NNF(Nearest Neighbor Filter??) only takes into account the prediction of the existing track from the last frame and the new observation obtained from the sensor. For each new data set, every segment is assigned to the nearest previous track after predicting motions for previous tracks from previous measurements to the current measurement. 

[61]에서는 Range image를 이용하여서 군중들 추적을 연구 하였다. 사람의 위치를 **general dynamic model**로 표현할수 없어 **greedy nearest neighbor filter**를 이용 하였다. `Prassler, et al. introduced a people tracking system for a crowded scene [61]. Considering that a person’s location cannot be easily characterized by a general dynamic model, the algorithm had to rely almost entirely on the greedy nearest neighbor filter to track people for consecutive range images. The result indicate that this system could track 5 to 30 moving objects in real-time (Figure 2.14).`

![](https://i.imgur.com/d1DfkrB.png)

대부분의 레이져 기반 차량 추적 시스템에서는 **Mahalanobis distance as the proximity metric for GNN**를 채택하고 있다. `Most laser-based vehicle tracking systems usually apply the Mahalanobis distance as the proximity metric for GNN. The Mahalanobis Distance was introduced by P.C.Mahalanobis in 1936. `

이 방법은 유클리드 거리 방식대비 geometric정보를 사용하기에 채택 되었다. `This measurement is used instead of Euclidean distance because it considers the geometric information implicit in:`
- that they primarily move forward and not side-to-side.

![](https://i.imgur.com/T2yhrF7.png)


차량은 앞뒤로 만 움직이며 긴 좌표(거리)방향이 필요 하므로 적합하다. `For the 2-dimensional data, since the covariance matrix represents the axis of the ellipse covering the distribution of the data, it can represent the direction and size of the entire data cluster. For points with the same mean value of the Euclidean distances to every point in the data cluster, the ones near the long axis direction have a small Mahalanobis distance versus the ones near the short axis direction. This property is very useful for finding the corresponding feature points of a vehicle since the vehicle always tends to move towards the long axis direction. `


두 Metrics에 대한 비교는 아래에 설명 되어 있다. `The difference between the two metrics is illustrated by the following example.`

![](https://i.imgur.com/t5iQ6TS.png)

위 그림에서 원은 과거의 측정값(Measuremet)이고 start는  현재의 **two probable locations**이다. `In Figure 2.15, the circle points are a measurement of a vehicle in the last frame, and the star points represent two probable locations of the vehicle in the current frame. `

유클리드 방식으로는 A의 값이 더 작다. 차량으로써는 갑자기 방향을 바꿀수 없기 때문에 B가 더 현실적이다. `If the Euclidean distance is used to measure the distance, the Euclidean distance between the probably positions and the data set are D_e(A) = 252.5 and D_e(B) = 361.4. However, as a vehicle, point B should have a higher probability of being the next cluster position than point A since it´ s nearly impossible for a vehicle to suddenly move laterally. `

마할라노비스 방식으로는 B가 더 작다. `If the Mahalanobis distance is applied, then the distances become D_m(A) = 77.9 and D_m(B) = 6.6,`
- which illustrates that the association along the long axis of a data cluster tends to generate trajectories consistent with expected vehicle motion. 

비슷하게, 만약 궤적을 알고 있다면 마할라노비스 거리 방식은 가중치를 줄수 있다. `Similarly, if the trajectory of a cluster is known, the Mahalanobis distance metric can use weightings aligned with the expected trajectory. `

따라서 마할라노비스 방식이 더 좋다. `Thus, the Mahalanobis distance better associates new measurements to a vehicle projected along its probable path, not to vehicles that happen to be close to the new measurement but whose paths are not nearby the measurement [38].`

본 논문에서는 허용할만한 에러를 보이고 간단한 구현 방식으로 GNN 필터를 사용 하였다. `In this thesis, for easiness implementation with acceptable error, GNN filter is applied as data association approach.`

![](https://i.imgur.com/qw7nNeg.png)
![](https://i.imgur.com/s46YsoT.png)

---
