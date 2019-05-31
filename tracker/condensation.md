[CONDENSATION—Conditional Density Propagation for Visual Tracking](http://link.springer.com/article/10.1023/A:1008078328650)


- 그리고 Condensation 알고리즘이라는 개념이 Particle Filter의 일부분인지, 같은 개념인지도 궁금합니다.

 검색을 하다보니 Condensation 알고리즘이 Particle Filter를 기반한 것이라고 많이 봤는데

 카페에서 종종 같은 개념으로 여기기도 한다는 글을 봐서 명확하게 구분을 하고 싶습니다.



-대충 맞습니다. 실제로 linearity와 Gaussianity를 보이는 대상은 거의 없습니다. 따라서 대부분의 경우 PF가 KF보다 좋은 성능을 보입니다.

- condensation은 PF + deformable template 라고 보시면 됩니다. 컴퓨터비전에서의 contour 기반 추적을 위해 통계학적 기법인 PF를 가져다 쓴것이라고 보면 되고, 한마디로 PF가 이론이면 condensation은 응용입니다.

- 핵심 그림은 한 사이클(예측-관측-수정) 내에서 분포(울퉁불퉁한 언덕들)이 변하는 그림입니다. 그거 이해하시면 90프로 이해한 겁니다. Monte Carlo 기법에 대해 개념만 알아두시면 많이 도움이 될겁니다



