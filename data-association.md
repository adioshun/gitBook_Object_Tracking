# Data Association

> 유사 표현?? Assignments Algorithm,  matching algorithm, Validation Gate (확인 필요)

정의 
    - 추적되고 있는 객체들에 올바른 관측치를 할당하는 것
    - assigning sensor responses to trajectories





하나의 물체에 대해서 중복되어 발생하는 트랙을 조정하는 기법이다.

이는 두 개 또는 그 이상의 트랙이 실제 같은 물체를 추적하고 있는 경우에 하나의 트랙으로 만들어주는 역할을 한다. 
이를 트랙간 연관(TTTA : Track To Track Association)기법이라 한다. 트랙간 연관이 이루어진 후 트랙간 융합(TTTF : Track To Track Fusion) 기법을 통해 다중센서로부터 획득된 트랙들을 결합하여 하나의 트랙을 형성하게 되면 단일센서로부터 얻어진 값보다 추정오차가 개선된 추적이 가능하다.

이러한 중복된 트랙을 인지하고 삭제하기 위해 
- MHT(Multiple Hypothesis Tracking) 알고리듬에서는 N-scan back을 수행하여 같은 측정치를 연속적으로 사용하고 비슷한 상태 벡터를 사용하는 경우 트랙을 병합하여 트랙을 정확히 추정한다. 
- 그러나 대부분 사용하는 NNF, PDAF, JPDAF, IPDAF, LM-IPDAF등의 알고리듬은 No-scan back이다. 

---

## [Udacity](https://www.youtube.com/watch?v=DK1DIcPwCOU)





---

# [Robotics 2 Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf)

![](https://i.imgur.com/DGFjhYz.png)

- 데이터 수집 
- 측정값 예측 : 탐지 대상이 있을것 같은 **Area** 생성 
    - Area : Validation Gate라고 불리우며, 탐색 범위를 좁힐때 사용 됨   
- 측정값이 Area안에 있는지 확인 


#### 절차 #1 (Multi-Target DA: Global NN)

1. Build the assignment matrix
2. Solve the linear assignment problem 
    - Hungarian method (blow up to square matrix)
    - Munkres algorithm for rectangular matrices
    - Finds global cost minimum! 
3. Check if assignments are in the validation gate
4. Performs DA jointly!


### 절차 #2 

prediction: propagate state pdf forward in time,taking process noise into account (translate, deform,and spread the pdf)

Data association to determine best match

update: use Bayes theorem to modify prediction pdf based on current measuremen






---
