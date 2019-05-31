# [Robotics 2 Target Tracking](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-12-tracking.pdf)

![](https://i.imgur.com/suq6cyL.png)


---

일반적으로 단일 객체 추적에 적용

Teichman의 연구\[7\]에선 단일 칼만 필터기반 추적기법을 이용하여 데이터를 누적시켜 분류의 성능을 높이고자 했다.

하지만 물체가 몇 개 없는 단조로운 시나리오에서 전후 프레임 간에 일치되는 물체관계를 이미 알고 있다고 가정하여, 특별한 데이터 연계 방법 없이 해당 물체 정보들을 단일 칼만 필터만 사용해추적 및 누적하여 포인트 수 증가를 유도하였다.

```
[7] A. Teichman, J. Levinson and S. Thrun, “Towards 3D Object Recognition via Classification of Arbitrary Object Tracks,” International Conference on Robotics and Automation, Shanghai, China, May 2011.
```



---
# [Udacity - Kalman as a tracker](https://classroom.udacity.com/courses/ud810/lessons/3325568562/concepts/33096785930923)