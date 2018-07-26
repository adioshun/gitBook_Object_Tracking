# 이미지 기반 트래킹 

 [A Review on Object Detection and Tracking Methods](https://ijrest.net/downloads/volume-2/issue-1/pid-21201506.pdf) : 2015


### [A Survey on Object Detection and Tracking Methods](https://pdfs.semanticscholar.org/25a6/c5dff9a7019475daa81cd5a7f1f2dcdb5cf1.pdf): 2014

![image](https://user-images.githubusercontent.com/17797922/40040388-0ac64296-5855-11e8-8b14-5b15cc508410.png)


### [A Review of Object Detection and Tracking Methods](http://www.ijaerd.com/papers/finished_papers/A%20Review%20of%20Object%20Detection%20and%20Tracking%20Methods-IJAERDV04I1045913.pdf):2017

![image](https://user-images.githubusercontent.com/17797922/40040689-303d1cce-5856-11e8-86c5-07293af6f9ec.png)

- Tracking Methods
    - Region-based tracking methods
    - contour tracking methods
    - 3D Model based tracking methods
    - Feature based tracking methods
    - Color and Pattern based tracking methods

> [Moving Object Tracking of Vehicle Detection”: A Concise Review](http://docplayer.net/16497156-Moving-object-tracking-of-vehicle-detection-a-concise-review.html): 2015

---

색상객체의 추적에 사용되는 대표적인 추적 알고 리즘은 
- Mean Shift, 
- CAMshift, 
- ABCshift, 
- 칼만 필터, 
- 비선형 칼만 필터, 
- 입자 필터 

그 중 Mean Shift, CAMshift ABCshift 알고리즘은 탐색 윈도우 를 통하여 추적물체의 영역 및 중심을 계산한다.

Mean Shift(평균이동알고리즘)는 
- 데이터 집합의 밀도분포를 기반으로 관심영역 객체를 고속으로 추적하는 알고리즘으로서 초기의 검색 영역의 크기와 위치를 지정하면 반복적인 색 분할 계산으로 색상 클러스터가 발생하고 초기 지정한 색 영역에 기반을 두어경계를 결정하여 관심 물체를 추출하게 된다[4].

Mean Shift 알고리즘을 개량한 CAMshift 알고리즘은 1998년 GR Gradski에 의해 처음 소개되었다[5]. 
- Color Segment 방법의 Mean Shift 알고리즘을 연속적인 입력 영상에서 사용하기 위해 개선한 것으로 탐색 윈도우의 크기를 스스로 조정하는 기법을 사용하여 능동적으로 변화하는 객체의 크기를 검출하고 추적해낼 수 있다. 

ABCshift 알고리즘은 
- CAMshift 방법과 유사하나 복잡한 색상의 배경에 적응하여 객체를 배경과 따로 분리하는 효과를 얻어서 객체와 같은 색상이 등장하는 상황 중에도 강인한 추적을 보인다[7]. 　


칼만 필터, 확장 칼만 필터, 입자 필터는 오차가 포함된 현재 시스템 측정값이나 관측값을 바탕으로 미래정보를 예측하는 알고리즘이다. 

칼만 필터는 루프만 칼만에 의해 1960년대 초 개발된 필터로 순환적선형구조로 되어 있고 단순하며 수렴 성이 좋다. 

칼만 필터는 수식을 이용하여 직접적인 예측이 가능하므로 컴퓨터 시스템을 이용하여 추적할 때 적합한 방법이다[8]. 

그리고 입자 필터(Particle Filter)를 이용한 추적은 시스템에 가우시안 확률분포로 임의로 생성된 입력을 종합하여 추적이 이루어지도록 하는 방법이다. 
- Particle Filter 알고리즘은 객체가 가려지는 상황에 강인하므로, 이 특성을 이용한 부분색상정보 기반의 추적 시스템이 개발되었다[9]. 
- 일반적으로 물체의 선형적인 운동에는 칼만 필터가 사용되고 비선형적 운동에는 확장 칼만 필터나 입자 필터가 사용된다. 

Manya Afonso는 대표적인 비선형 예측 알고리즘인 확장 칼만 필터와 입자 필터에 대해 비교 분석하였다[10].


혼합방식 : 위에 소개된 알고리즘들이 갖고 있는 장점을 취하고 단점을 보완하기 위해 각각의 알고리즘을 통합하여 객체를 추적하려는 시도도 이루어지고 있다. 

그예로 칼만 필터와 CAMshift 알고리즘을 결합하여 추적객체의 가려짐에 강건한 추적에 관한 연구가 진행되었다[11,12]. 
- 탐색 윈도우 예측 시 물체의 속도만을 반영하고 CAMshift에 의해 구한 중심벡터 이동정보를 활용하지는 않았다. 

색상객체의 추적을 위한 또 다른 추적모듈 결합방법으로 칼만 필터와 입자 필터의 결합에 대해 다룬논문도 소개되었다[13]. 
- 선형 필터인 칼만 필터는 선형 운동을 하는 객체의 추적을, 비선형 운동을 하는 객체의 추적은 입자 필터를 이용하여 추적한 점이특징이다. 

또한, 추적되는 색상객체를 SURF 알고리즘을 이용하여 인식하고 칼만 필터를 결합하여 움직임을 예측한 방법도 연구된 바가 있다[14].

> CAMshift 기법과 칼만 필터를 결합한 객체 추적 시스템, 김대영, 2013

---



