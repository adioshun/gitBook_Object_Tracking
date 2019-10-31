# [Introduction to Data Association

목적 : Gating to determine possible matching observations

정의 : A method for pruning matches that are geometrically unlikely from the start.


|![](https://i.imgur.com/c2uEroB.png)|![](https://i.imgur.com/26AA2O4.png)|
|-|-|

## Data Association Scores

- Similarity or affinity scores for determining the correspondence of blobs across frames is based on feature similarity between blobs.

- Commonly used features: location , size / shape, velocity, appearance

- For example: location, size and shape similarity can be measured based on bounding box overla(IoU)

---

# Validation Gate 

- The area around the predicted measurement in which pairings are accepted is called validation gate or validation region

- This procedure is also called validation gaiting or simply gaiting 




Validation Gate 방법 
 - Euclidian distance : Position(O), Uncertainty(x), Correlations (x)
 - Mahalanobis distance with diagonal covariance matrices : Position(O), Uncertainty(o), Correlations (x)
 - Mahalanobis distance : Position(O), Uncertainty(O), Correlations (O)
 
 


---

- [Gating](http://srl.informatik.uni-freiburg.de/teachingdir/ws13/slides/11-TemporalReasoning-3.pdf): 강추, ppt, 83page 
- [[Uni Freiburg] Robotics 2 Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf)
- [[CSE598C] Robotics 0 Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/comboptBlockICM.pdf)
- [[CSE598C] Robotics 1 Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf)
- [[CSE598C] Robotics 2 Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart2.pdf)






