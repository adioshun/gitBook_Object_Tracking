```Python

import cv2
import numpy as np

#  create an empty frame, of size 800 x 800
frame = np.zeros((800, 800, 3), np.uint8)

#initialize the arrays that will take the coordinates of the measurements and predictions of the mouse movements
last_measurement = current_measurement = np.array((2,1),np.float32)
last_prediction = current_prediction = np.zeros((2,1), np.float32)

def mousemove(event, x, y, s, p):
    """
    we store the last measurements and last prediction,
    correct the Kalman with the current measurement, calculate the Kalman prediction,
    and finally draw two lines, from the last measurement to the current and from the last prediction to the current:
    """
    global frame, current_measurement, measurements, last_measurement, current_prediction, last_prediction

    last_prediction = current_prediction
    last_measurement = current_measurement

    current_measurement = np.array([[np.float32(x)],[np.float32(y)]])  #마우스 입력

    # Update(=correction): In the second phase, it records the object's position and adjusts the covariance for the next cycle of calculations   
    kalman.correct(current_measurement)

    # Predict: In the first phase, the Kalman filter uses the covariance calculated up to the current point in time to estimate the object's new position
    current_prediction = kalman.predict()

    lmx, lmy = last_measurement[0], last_measurement[1]
    cmx, cmy = current_measurement[0], current_measurement[1]
    lpx, lpy = last_prediction[0], last_prediction[1]
    cpx, cpy = current_prediction[0], current_prediction[1]

    cv2.line(frame, (lmx, lmy), (cmx, cmy), (0,100,0))
    cv2.line(frame, (lpx, lpy), (cpx, cpy), (0,0,200))
    """
    Parameters:
    img – 그림을 그릴 이미지 파일
    start – 시작 좌표(ex; (0,0))
    end – 종료 좌표(ex; (500. 500))
    color – BGR형태의 Color(ex; (255, 0, 0) -> Blue)
    thickness (int) – 선의 두께. pixel
    """


#  initialize the window and set the Callback function.
cv2.namedWindow("kalman_tracker")
cv2.setMouseCallback("kalman_tracker", mousemove)

kalman = cv2.KalmanFilter(4,2)
    """
    - dynamParams: This parameter states the dimensionality of the state
    - MeasureParams: This parameter states the dimensionality of the measurement
    - ControlParams: This parameter states the dimensionality of the control
    - vector.type: This parameter states the type of the created matrices that should be CV_32F or CV_64F
    """
kalman.measurementMatrix = np.array([[1,0,0,0],[0,1,0,0]],np.float32)
kalman.transitionMatrix = np.array([[1,0,1,0],[0,1,0,1],[0,0,1,0],[0,0,0,1]],np.float32)
kalman.processNoiseCov = np.array([[1,0,0,0],[0,1,0,0],[0,0,1,0],[0,0,0,1]],np.float32) * 0.03

while True:
    cv2.imshow("kalman_tracker", frame)
    if (cv2.waitKey(30) & 0xFF) == 27:
        break
cv2.destroyAllWindows()



```


---

```Python
#!/usr/bin/env python
"""
   Tracking of rotating point.
   Rotation speed is constant.
   Both state and measurements vectors are 1D (a point angle),
   Measurement is the real point angle + gaussian noise.
   The real and the estimated points are connected with yellow line segment,
   the real and the measured points are connected with red line segment.
   (if Kalman filter works correctly,
    the yellow segment should be shorter than the red one).
   Pressing any key (except ESC) will reset the tracking with a different speed.
   Pressing ESC will stop the program.
"""
# Python 2/3 compatibility
import sys
PY3 = sys.version_info[0] == 3

if PY3:
    long = int

import cv2 as cv
from math import cos, sin, sqrt
import numpy as np

if __name__ == "__main__":

    img_height = 500
    img_width = 500
    kalman = cv.KalmanFilter(2, 1, 0)

    code = long(-1)

    cv.namedWindow("Kalman")

    while True:
        state = 0.1 * np.random.randn(2, 1)

        kalman.transitionMatrix = np.array([[1., 1.], [0., 1.]])
        kalman.measurementMatrix = 1. * np.ones((1, 2))
        kalman.processNoiseCov = 1e-5 * np.eye(2)
        kalman.measurementNoiseCov = 1e-1 * np.ones((1, 1))
        kalman.errorCovPost = 1. * np.ones((2, 2))
        kalman.statePost = 0.1 * np.random.randn(2, 1)

        while True:
            def calc_point(angle):
                return (np.around(img_width/2 + img_width/3*cos(angle), 0).astype(int),
                        np.around(img_height/2 - img_width/3*sin(angle), 1).astype(int))

            state_angle = state[0, 0]
            state_pt = calc_point(state_angle)

            prediction = kalman.predict()
            predict_angle = prediction[0, 0]
            predict_pt = calc_point(predict_angle)

            measurement = kalman.measurementNoiseCov * np.random.randn(1, 1)

            # generate measurement
            measurement = np.dot(kalman.measurementMatrix, state) + measurement

            measurement_angle = measurement[0, 0]
            measurement_pt = calc_point(measurement_angle)

            # plot points
            def draw_cross(center, color, d):
                cv.line(img,
                         (center[0] - d, center[1] - d), (center[0] + d, center[1] + d),
                         color, 1, cv.LINE_AA, 0)
                cv.line(img,
                         (center[0] + d, center[1] - d), (center[0] - d, center[1] + d),
                         color, 1, cv.LINE_AA, 0)
            """

            img – 그림을 그릴 이미지 파일
            start – 시작 좌표(ex; (0,0))
            end – 종료 좌표(ex; (500. 500))
            color – BGR형태의 Color(ex; (255, 0, 0) -> Blue)
            thickness (int) – 선의 두께. pixel
            """


            img = np.zeros((img_height, img_width, 3), np.uint8)
            draw_cross(np.int32(state_pt), (255, 255, 255), 3) #white
            draw_cross(np.int32(measurement_pt), (0, 0, 255), 3) #blue
            draw_cross(np.int32(predict_pt), (0, 255, 0), 3) # green
            print("state_pt : {}".format(state_pt))
            print("measurement_pt : {}".format(measurement_pt))
            print("predict_pt : {}".format(predict_pt))

            #cv.line(img, state_pt, measurement_pt, (0, 0, 255), 3, cv.LINE_AA, 0)
            #cv.line(img, state_pt, predict_pt, (0, 255, 255), 3, cv.LINE_AA, 0)

            kalman.correct(measurement)

            process_noise = sqrt(kalman.processNoiseCov[0,0]) * np.random.randn(2, 1)
            state = np.dot(kalman.transitionMatrix, state) + process_noise

            cv.imshow("Kalman", img)

            code = cv.waitKey(100)
            if code != -1:
                break

        if code in [27, ord('q'), ord('Q')]:
            break

    cv.destroyWindow("Kalman")

```
