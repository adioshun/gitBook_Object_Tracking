m-out-of-n기법 : n번 스캔에서 m번 연관된 정도를 살핌, 5회 미만 assign 실패시 Dead로 판단
- NNF(Nearest Neighbor Filter), PDAF(Probabilistic Data Association Filter), JPDAF(Joint PDA)


확률 기반 기법 : 연관필터에서 제공하는 존재 확률 기법 활용 
- IPDAF(Integrated PDAF)이나 LM-IPDAF(Linear-Multiple IPDA) 기법


---


하나의 물체에 대해서 중복되어 발생하는 트랙을 조정하는 기법이다.

이는 두 개 또는 그 이상의 트랙이 실제 같은 물체를 추적하고 있는 경우에 하나의 트랙으로 만들어주는 역할을 한다. 
이를 트랙간 연관(TTTA : Track To Track Association)기법이라 한다. 트랙간 연관이 이루어진 후 트랙간 융합(TTTF : Track To Track Fusion) 기법을 통해 다중센서로부터 획득된 트랙들을 결합하여 하나의 트랙을 형성하게 되면 단일센서로부터 얻어진 값보다 추정오차가 개선된 추적이 가능하다.

이러한 중복된 트랙을 인지하고 삭제하기 위해 
- MHT(Multiple Hypothesis Tracking) 알고리듬에서는 N-scan back을 수행하여 같은 측정치를 연속적으로 사용하고 비슷한 상태 벡터를 사용하는 경우 트랙을 병합하여 트랙을 정확히 추정한다. 
- 그러나 대부분 사용하는 NNF, PDAF, JPDAF, IPDAF, LM-IPDAF등의 알고리듬은 No-scan back이다. 



