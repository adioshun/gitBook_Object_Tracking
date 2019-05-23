### CAM(Continuously Adaptive Mean) shift 상세 

특징 : Mean shift의 문제점 중 ROI크기가 일정하다는 문제점을 해결하여 ROI크기가 매번 바뀔 수 있고,회전변화에도 추적이 가능하다.
- 탐색윈도우의 크기를 스스로 조정하는 기법을 사용하여 Mean-shift의 답점을 보강한다.


검출된 객체의 영역의 Hue 값의 분포를 이용하여 변화될 위치를 예측하고 탐지한 후 중심을 찾아 객체를 추적하게 된다. 
- 상대적으로 Hue 값을 사용하면 조명의 영향에 덜 민감하므로 Hue값을 사용한다


단점 : 조도변화, 잡음이 많은 배경에서는 성능이 좋지않은 특징

![](https://i.imgur.com/CZeuyTR.png)

단계
1. 관심영역(ROI)이 주어지면 HSV 색 모델의 Hue값으로 변환한다. 
2. ROI에서 1차원 histogram을 구축하여 저장하고 추적 모델로 사용한다.
3. ?

---

[비디오 처리 - MeanShift, CamShift](https://blog.naver.com/warchife/221136545517)

[[영상추적#1] Mean Shift 추적](http://darkpgmr.tistory.com/64?category=460965)

[OpenCV의 MeanShift / CamShift 추적기](http://darkpgmr.tistory.com/111): C++코드 

[비디오에서 객체 추적하기1 -  Meanshift 살펴보기](http://sams.epaiai.com/220658244422) : python

[비디오에서 객체 추적하기2 - CamShift](http://sams.epaiai.com/220659310860): python

[[Object Tracking] OpenCV 객체추적 프로그램 접근법 (MeanShift and CAMShift)](https://eehoeskrap.tistory.com/41?category=570078): Enough is not enough