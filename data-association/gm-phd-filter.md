
GM-PHD 필터

> [GM-PHD 필터를 이용한 보행자 탐지 성능 향상 방법](http://www.dbpia.co.kr/Article/NODE06594856), 2015


[GM-PHD filter implementation in python (Gaussian mixture probability hypothesis density filter)](https://github.com/danstowell/gmphd): N. Vo and W. K. Ma. The gaussian mixture probability hypothesis density filte, 2006
- 설명 : http://www.mcld.co.uk/blog/2013/update-on-gm-phd-filter-with-python-code.html
- [GMPHD-py with its application to underwater robotic mapping](https://github.com/tfabbri/gmphd-py)

- [Python Particle Probability Hypothesis Density Filter](): B.-N. Vo, S. Singh, and A. Doucet, “Sequential Monte Carlo implementation     of the PHD filter for multi-target tracking,”, 2003


[Multi-target Tracking with PHD Filters](https://www.math.u-bordeaux.fr/~mpace/PhdFiltering.html)

---

본 논문에서는 앞서 언급한 문제를 극복하고자 확률밀도가정(Probability Hypothesis Density (PHD))필터를 이용하여 영
상기반의 온라인 다중객체추적을 구현한다. 

PHD 필터는 다중 객체와 측정치들을 Random Finite Set에 근거하여 객체 집합과 관측치 집합으로 모델링한다. 

기존의 데이터연관 기반의 추적 방식들과 다르게 PHD 필터는 각 객체를 독립적으로 추정하기 보다 객체들을 하나의 집합으로 고려하여 추정한다. 

이러한 특징 때문에 각 객체에 하나의 관측지를 할당하는 **데이터연관 부분이 불필요**하다. 

또한, PHD 필터는 객체의 사라짐, 출현, 그리고 검출 불확실성을 확률적으로 모델링하여 표적 객체 관리와 검출 불확실성 관리를 필터링 과정에서 자동적으로 처리할 수 있다는 장점이 있다.



