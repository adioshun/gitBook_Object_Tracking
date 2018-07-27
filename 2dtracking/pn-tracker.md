# PN tracker

> [[영상추적#2] TLD - 추적하면서 학습한다](http://darkpgmr.tistory.com/65)

영국 Surrey 대학의 Zdenek Kalal

"P-N Learning: Bootstrapping Binary Classifiers by Structural Constraints", CVPR2010
"Tracking-Learning-Detection", PAMI2012

https://www.youtube.com/watch?v=1GhNXHCQGsM#action=share


TLD 회사 홈페이지: http://tldvision.com/index.html

TLD 소스코드: https://github.com/zk00006/OpenTLD

OpenTLD : https://github.com/zk00006/OpenTLD

TLD(Tracking-Learning-Detection)라는 새로운 추적 프레임워크를 제안했기 때문입니다.
- TLD는 말 그대로, 추적하면서 학습함으로써 detection이 가능한 추적기라는 의미


PN tracker는 내부적으로 tracker와 detector를 동시에 운용합니다. 
- tracker로는 optical flow tracker를 사용하고 
- detector로는 [ferns](http://darkpgmr.tistory.com/90)를 사용

절차 
1. 처음에 사용자가 추적할 대상 영역을 설정해 주면 tracker와 detector가 동시에 초기화가 됩니다. 이 때, detector의 경우에는 처음 입력 영상 영역 하나에 대해서만 학습이 되는 셈입니다.
2. 이후 입력 영상이 들어오면 tracker로도 대상을 찾고, detector로도 대상을 찾습니다. 만일 tracker가 성공했다면 tracker로 찾는 윈도우(window) 영역이 detector의 학습 데이터로 활용되어 detector를 좀더 강력하게 해 줍니다. 뿐만 아니라, detector가 찾은 영역들 중에서 tracker 결과와 일치하지 않는 것들은 오검출로 분류되어 detector를 학습시키기 위한 negative example로 활용됩니다.
3. 만일 tracker가 실패한 경우에는 detector가 성공할 때까지 기다렸다가, detector가 성공하면 검출된 위치로 tracker를 초기화하고 다시 추적을 시작하는 것입니다.


|detector(검출기)|미리 알고있는(학습된) 대상을 입력 영상에서 찾을 수 있는 방법인데, 아무 영상이나 이미지 1장만 주어져도 대상을 찾을 수 있어야 합니다.|
|-|-|
|tracker(추적기)|일반적으로 동영상의 인접한 영상 프레임들 사이의 시간적, 공간적, 형태적 유사성을 이용하여 대상을 찾는 기술<br>최근의 추적 정보를 활용하기 때문에 만일 대상의 크기, 형태, 위치 등이 급격히 변할 경우에는 실패할 확률이 매우 높아진다|
