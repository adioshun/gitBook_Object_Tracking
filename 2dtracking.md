# 이미지 기반 트래킹 

- [A Review on Object Detection and Tracking Methods](https://ijrest.net/downloads/volume-2/issue-1/pid-21201506.pdf) : 2015



- [A Survey on Object Detection and Tracking Methods](https://pdfs.semanticscholar.org/25a6/c5dff9a7019475daa81cd5a7f1f2dcdb5cf1.pdf): 2014

    ![image](https://user-images.githubusercontent.com/17797922/40040388-0ac64296-5855-11e8-8b14-5b15cc508410.png)


- [A Review of Object Detection and Tracking Methods](http://www.ijaerd.com/papers/finished_papers/A%20Review%20of%20Object%20Detection%20and%20Tracking%20Methods-IJAERDV04I1045913.pdf):2017

    ![image](https://user-images.githubusercontent.com/17797922/40040689-303d1cce-5856-11e8-86c5-07293af6f9ec.png)

- [Moving Object Tracking of Vehicle Detection”: A Concise Review](http://docplayer.net/16497156-Moving-object-tracking-of-vehicle-detection-a-concise-review.html): 2015
    - Tracking Methods
        - Region-based tracking methods
        - contour tracking methods
        - 3D Model based tracking methods
        - Feature based tracking methods
        - Color and Pattern based tracking methods


색상객체의 추적에 사용되는 대표적인 추적 알고 리즘은 
- Mean Shift, 
- CAMshift, 
- ABCshift, 
- 칼만 필터, 
- 비선형 칼만 필터, 
- 입자 필터 

그 중 Mean Shift, CAMshift ABCshift 알고리즘은 탐색 윈도우 를 통하여 추적물체의 영역 및 중심을 계산한다.
Mean Shift(평균이동알고리즘)는 데이터 집합의 밀
도분포를 기반으로 관심영역 객체를 고속으로 추적
하는 알고리즘으로서 초기의 검색 영역의 크기와 위
치를 지정하면 반복적인 색 분할 계산으로 색상 클러
스터가 발생하고 초기 지정한 색 영역에 기반을 두어
경계를 결정하여 관심 물체를 추출하게 된다[4].
Mean Shift 알고리즘을 개량한 CAMshift 알고리
즘은 1998년 GR Gradski에 의해 처음 소개되었다
[5]. Color Segment 방법의 Mean Shift 알고리즘을
연속적인 입력 영상에서 사용하기 위해 개선한 것으
로 탐색 윈도우의 크기를 스스로 조정하는 기법을
사용하여 능동적으로 변화하는 객체의 크기를 검출
하고 추적해낼 수 있다. 이 알고리즘의 응용사례로,
pan-tilt-zoom 카메라를 이용하여 객체를 검출하고
크기가 변하는 얼굴을 추적하기 위해서 CAMshift와
AAM(Active Appearance Model) 얼굴인식 알고리
즘을 사용한 감시 시스템이 구현되었다[6].
ABCshift 알고리즘은 CAMshift 방법과 유사하나
복잡한 색상의 배경에 적응하여 객체를 배경과 따로
분리하는 효과를 얻어서 객체와 같은 색상이 등장하
는 상황 중에도 강인한 추적을 보인다[7]. 　


