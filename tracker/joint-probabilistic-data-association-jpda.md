# [LIDAR-BASED MULTI-OBJECT TRACKING SYSTEM WITH DYNAMIC MODELING](https://neu-gou.github.io/thesis_Mengran.pdf): 2012, 석사 학위 논문

복합한 환경에서의 다중 물체 추적시 발생 가능한 association의 불확실성을 제거 하기 위해서는  JPDA가 모든 가능한 연관 확률 값을 고려하므로 유용하다. `To eliminate association ambiguity in complex scenes, especially for multi-objective tracking, JPDA is a data association algorithm that takes into account every possible association. `

이 방식은 센서로 탐지된 위치와 기존 Track간의 가능성을 **Bayesian estimate **을 계산하여 **hypothesis matrix **형태로 저장 한다. 이후 가장 높은 확률값을 가지고 있는것을 할당한다.  ` It computes the Bayesian estimate of the correspondence between segments detected by sensor and possible existing tracks and forms a hypothesis matrix including all possible associations. The assignments with highest probability are picked out. `

 [45, 62]에서는 최초로 JPDA를 적용하여 가능성을 보였다. `As an example of JPDA, Schulz applied sample-based JPDA in laser-based tracking system at first and showed its effectiveness for the multiple people tracking problem (Figure 2.16) [45, 62]. `

![](https://i.imgur.com/S3hU37H.png)


[46]에서는 JPDA를 수정한 방식을 제안 하였다. `By modifying JPDA to separate highly-correlated target-path combinations from poorly-correlated combinations, Frank, et al. proposed two extended JPDA approaches and tested them off-line (Figure 2.17) [46]. `

![](https://i.imgur.com/pH29bxg.png)


DARPA 2007 에서 JPDA가 이용되었다. `The robot in DARPA 2007 challenge, Junior, mentioned earlier in Section 2.2.2.2, also used this JPDA approach.`

---

