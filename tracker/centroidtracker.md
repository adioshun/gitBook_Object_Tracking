# The centroid tracking algorithm

> [Simple object tracking with OpenCV](https://www.pyimagesearch.com/2018/07/23/simple-object-tracking-with-opencv/): pyimagesearch, 2018 [[코드]](https://gist.github.com/adioshun/779738c3e28151ffbb9dc7d2b13c2c0a)


![](https://www.pyimagesearch.com/wp-content/uploads/2018/07/simple_object_tracking_step2.png)

- 보라색점 : 이전 탐지 결과 
- 노란색점 : 새 탐지 결과 
- 녹색선 : 유클리드 거리 



> rects = a tuple with this structure (startX, startY, endX, endY)


The goal is to track the objects and to maintain correct object IDs 
- this process is accomplished by computing the Euclidean distances 
 - between all pairs of `objectCentroids`  and `inputCentroids` , 
 - followed by associating object IDs that minimize the Euclidean distance.

```python
# grab the set of object IDs and corresponding centroids
objectIDs = list(self.objects.keys())
objectCentroids = list(self.objects.values())
 
# compute the distance between each pair of object
# centroids and input centroids, respectively -- our
# goal will be to match an input centroid to an existing
# object centroid
D = dist.cdist(np.array(objectCentroids), inputCentroids)
 
# in order to perform this matching we must (1) find the
# smallest value in each row and then (2) sort the row
# indexes based on their minimum values so that the row
# with the smallest value is at the *front* of the index
# list
rows = D.min(axis=1).argsort()
 
# next, we perform a similar process on the columns by
# finding the smallest value in each column and then
# sorting using the previously computed row index list
cols = D.argmin(axis=1)[rows]
```
