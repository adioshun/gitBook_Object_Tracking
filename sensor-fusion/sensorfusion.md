# Sensor fusion

[An extended Kalman Filter implementation in Python for fusing lidar and radar sensor measurements](https://github.com/mithi/Fusion-EKF-Python): mithi, python
- [Cpp버젼](https://github.com/mithi/fusion-ekf), [CPP버젼v2](https://github.com/mithi/fusion-ekf/tree/master/A-UPDATED-FUSIONEKF)
- [Object-Tracking-and-State-Prediction-with-Unscented-and-Extended-Kalman-Filters](https://github.com/srnand/Object-Tracking-and-State-Prediction-with-Unscented-and-Extended-Kalman-Filters) : 변형

[Extended Kalman Filter Project Starter Code](https://github.com/udacity/CarND-Extended-Kalman-Filter-Project): Udacity

[Object tracking with LIDAR, Radar, sensor fusion and Extended Kalman Filter](http://www.coldvision.io/2017/04/15/object-tracking-with-lidar-radar-sensor-fusion-and-extended-kalman-filter/): post

Sensor Fusion Algorithms For Autonomous Driving
- [Part 1 — The Kalman filter and Extended Kalman Filter](https://medium.com/@wilburdes/sensor-fusion-algorithms-for-autonomous-driving-part-1-the-kalman-filter-and-extended-kalman-a4eab8a833dd)



---

# Tool

[Data fusion development with ROS | BASELABS](https://www.baselabs.de/data-fusion-development-with-ros/)




---

```

[L(for lidar)] [m_x] [m_y] [t] [r_x] [r_y] [r_vx] [r_vy]
[R(for radar)] [m_rho] [m_phi] [m_drho] [t] [r_px] [r_py] [r_vx] [r_vy]

Where:
(m_x, m_y) - measurements by the lidar
(m_rho, m_phi, m_dho) - measurements by the radar in polar coordinates
(t) - timestamp in unix/epoch time the measurements were taken
(r_x, r_y, r_vx, r_vy) - the real ground truth state of the system

Example:
R 8.60363 0.0290616 -2.99903  1477010443399637  8.6 0.25  -3.00029  0
L 8.45  0.25  1477010443349642  8.45  0.25  -3.00027  0 

```

In this project the LIDAR measurements are transformed from the cartesian into the polar coordinate system using this formula:



![](http://www.coldvision.io/wp-content/uploads/2017/04/object_tracking_rada_measurements_transform.png)