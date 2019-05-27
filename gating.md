# [Introduction to Data Association](http://www.cse.psu.edu/~rtc12/CSE598C/datassocPart1.pdf)

목적 : Gating to determine possible matching observations

정의 : A method for pruning matches that are geometrically unlikely from the start.


![](https://i.imgur.com/c2uEroB.png)

![](https://i.imgur.com/26AA2O4.png)

## Data Association Scores

- Similarity or affinity scores for determining the correspondence of blobs across frames is based on feature similarity between blobs.

- Commonly used features: location , size / shape, velocity, appearance

- For example: location, size and shape similarity can be measured based on bounding box overla(IoU)

---

# [Robotics 2 Data Association](http://ais.informatik.uni-freiburg.de/teaching/ws09/robotics2/pdfs/rob2-11-dataassociation.pdf)

Validation Gate 방법 
 - Euclidian distance : Position(O), Uncertainty(x), Correlations (x)
 - Mahalanobis distance with diagonal covariance matrices : Position(O), Uncertainty(o), Correlations (x)
 - Mahalanobis distance : Position(O), Uncertainty(O), Correlations (O)
 
 
