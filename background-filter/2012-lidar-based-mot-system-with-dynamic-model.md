2.2.2.1 Background subtraction

Background subtraction techniques have been widely used for detecting moving objects from static cameras [23]. 

```
[23] M. Piccardi, “Background subtraction techniques: A review,” IEEE International Conference on Systems, Man and Cybernetics, 2004, pp. 3099–3104
```

One approach, presented by Fod et,al., considers the different features provided by LIDAR within a background model based on range information [24]. 

```
[24] A. Fod, A. Howard, and M. J. Mataric, “Laser-based people tracking,” IEEE International Conference on Robotics and Automation, Washington DC, May, 2002, pp. 3024–3029
```

In order to simultaneously detect moving targets and maintain the position of stationary objects, an occupancy grid map is employed to detect moving objects [25]. 

```
[24] A. Fod, A. Howard, and M. J. Mataric, “Laser-based people tracking,” IEEE International Conference on Robotics and Automation, Washington DC, May, 2002, pp. 3024–3029
```

The grid-based map technique has been widely used in Simultaneous Localization and Mapping (SLAM) for representing complex outdoor environments (Figure 2.1) [7, 35, 59]. 


```
[7] C. C. Wang, “Simultaneous localization, mapping and moving object tracking,” PhD thesis, The Robotics Institute, Carnegie Mellon University, Pittsburgh, PA, Apr. 2004
[35] T. D. Vu, O. Aycard, and N. Appenrodt, “Online localization and mapping with moving object tracking in dynamic outdoor environments,” IEEE Intelligent Vehicles Symposium, Istanbul, Turkey, June 2007
[59] T. D. Vu and O. Aycard, “Laser-based detection and tracking moving objects using data-driven markov chain monte carlo,” IEEE International Conference on Robotics and Automation, Kobe, Japan, May 2009

```


Due to the few features extracted from LIDAR data, by building motion-map and stationary-map separately, Wang showed this approach is more robust than a feature-based approach (Figure 2.1) [7].

