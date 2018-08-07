번 15년 1학기 석사입학을 앞둔 학생입니다.

패턴인식 개론 책을 보면서 공부함과 동시에 Particle Filter 를 관련하여 공부를 하는 중입니다.

따라서 Condensation 알고리즘과 관련한 논문을 보고 있습니다.

(CONDENSATION—Conditional Density Propagation for Visual Tracking)

(http://link.springer.com/article/10.1023/A:1008078328650)



제가 아직 입문시기다 보니 논문 읽는 법도 제대로 모르겠고, 개념에 대해서도 따로 배운 적이 없어서 몇가지 질문 및 부탁드리고자 글을 적게 됐습니다.



- Kalman Filter 와 Particle Filter의 차이가

 트래킹하고자 하는 대상의 데이터가

 선형구조(Linear System)이면서 가우시안분포(Gaussian density)일 때 그리고 각각이 아닐 때에 따라서

 두 필터를 상황에 맞게 사용하는 것이라 이해했는데 제가 이해한 것이 맞는지 여쭙고 싶습니다.



- 그리고 Condensation 알고리즘이라는 개념이 Particle Filter의 일부분인지, 같은 개념인지도 궁금합니다.

 검색을 하다보니 Condensation 알고리즘이 Particle Filter를 기반한 것이라고 많이 봤는데

 카페에서 종종 같은 개념으로 여기기도 한다는 글을 봐서 명확하게 구분을 하고 싶습니다.



- 마지막으로, 위에서 언급한 논문을 읽어보신 분이 계신다면, 이해를 위해서

 꼭 알아야할 개념이나 논문 속에서 언급된 내용 중에 특정 부분을 어디를 이해해야하는지(수식이나 Figure 등...)

 알려주실 수 있다면 꼭 좀 부탁드립니다...



매 학기 마다 Particle Filter에 대한 발표가 있지만 매번 Reference가 다르기도 하고

아직 랩실에 나온지 얼마 안되서 그런지 선배님한테 질문을 하기에도 애매한 상황이네요...



꼭좀 부탁드립니다!! 글 읽어주셔서 감사합니다~

[출처] Condensation 알고리즘 질문입니다~ (OpenCV KOREA 대한민국 최고의 컴퓨터비젼 커뮤니티) |작성자 aabbccdd


-대충 맞습니다. 실제로 linearity와 Gaussianity를 보이는 대상은 거의 없습니다. 따라서 대부분의 경우 PF가 KF보다 좋은 성능을 보입니다.
- condensation은 PF + deformable template 라고 보시면 됩니다. 컴퓨터비전에서의 contour 기반 추적을 위해 통계학적 기법인 PF를 가져다 쓴것이라고 보면 되고, 한마디로 PF가 이론이면 condensation은 응용입니다.
- 핵심 그림은 한 사이클(예측-관측-수정) 내에서 분포(울퉁불퉁한 언덕들)이 변하는 그림입니다. 그거 이해하시면 90프로 이해한 겁니다. Monte Carlo 기법에 대해 개념만 알아두시면 많이 도움이 될겁니다
[출처] Condensation 알고리즘 질문입니다~ (OpenCV KOREA 대한민국 최고의 컴퓨터비젼 커뮤니티) |작성자 aabbccdd
