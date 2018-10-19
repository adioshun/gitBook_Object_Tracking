# The Multiple Object Tracking Benchmark

https://motchallenge.net/

## Detection File
```
#  detection 2D file is
1,-1,463,433,73.864,167.61,71.405,-1,-1,-1
1,-1,807,419,30.903,70.127,69.018,-1,-1,-1
1,-1,1474,407,79.918,181.35,42.996,-1,-1,-1
1,-1,399,429,26,59,31.164,-1,-1,-1
1,-1,1173,410,43.624,98.993,30.971,-1,-1,-1
1,-1,1363,394,79.918,181.35,29.228,-1,-1,-1
```

![](https://i.imgur.com/vlKnkLn.png)

- 1, The first number indicates in which frame the object appears, 


- 2, second number identifies that object as belonging to a trajectory by assigning a unique ID (set to −1 in a detection file, as no ID is assigned yet). 
    - Each object can be assigned to only one trajectory. 
    - 식별 ID, -1이면 ID가 아직 할당되지 않은것, Detection파일에서는 모두 -1인듯 Annotation파일에서는 ID존재 


- 3~6, The next four numbers indicate the position of the bounding box of the pedestrian in 2D image coordinates. 
    - The position is indicated by the top-left corner as well as width and height of the bounding box. 


- 7, This is followed by a single number, which in case of detections denotes their **confidence score**. 

- 8~10, The last three numbers indicate the 3D position in real-world coordinates of the pedestrian. 
    - This position represents the feet of the person. 
    - In the case of 2D tracking, these values will be ignored and can be left at −1


## Annotation File 
```
# An example of such an annotation 2D file is:
1, 1, 794.2, 47.5, 71.2, 174.8, 1, -1, -1, -1
1, 2, 164.1, 19.6, 66.5, 163.2, 1, -1, -1, -1
1, 3, 875.4, 39.9, 25.3, 35.0, 0, -1, -1, -1
2, 1, 781.7, 25.1, 69.2, 170.2, 1, -1, -1, -1
```
- the 7th value (confidence score) acts as a flag whether the entry is to be considered. 
    - A value of 0 means that this particular instance is ignored in the evaluation, 
    - while a value of 1 is used to mark it as active.


> [MOTChallenge 2015: Towards a Benchmark for Multi-Target Tracking](https://arxiv.org/pdf/1504.01942.pdf)


---

# Welcome to the [UA-DETRAC](https://detrac-db.rit.albany.edu/) Benchmark Suite!

![](https://detrac-db.rit.albany.edu/index_files/examples.jpg)

- [UA-DETRAC: A New Benchmark and Protocol for Multi-Object Detection and Tracking](https://arxiv.org/abs/1511.04136): 2015, 

---

[TrackingNet: A Large-Scale Dataset and Benchmark for Object Tracking in the Wild](http://openaccess.thecvf.com/content_ECCV_2018/html/Matthias_Muller_TrackingNet_A_Large-Scale_ECCV_2018_paper.html), ECCV2018

https://tracking-net.org/