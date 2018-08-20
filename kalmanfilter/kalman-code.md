[추천 : Opencv3 target motion detection(From basic to Kalman)](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/463878/)



코드 설명 : https://cafe.naver.com/opencv/13685, https://cafe.naver.com/opencv/1634


최종적으로는
1. cvKalmanPredict 라는 함수를 이용하여 예측(과거 정보 이용)을 하고
2. cvKalmanCorrect라는 함수로 보정(현재 측정정보 이용)을 합니다.
3. 그리고 이 보정값은 다시 cvKalmanPredict 의 인자로 들어가는 반복구조입니다.


---

![](https://i.imgur.com/XskJiOx.png)

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


---

![](https://i.imgur.com/h8Lgnya.png)

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



---

![](https://i.imgur.com/PndfH0m.png)


```python
#! /usr/bin/python

"""Surveillance Demo: Tracking Pedestrians in Camera Feed
https://github.com/techfort/pycv/blob/master/chapter8/surveillance_demo/main.py

The application opens a video (could be a camera or a video file)
and tracks pedestrians in the video.

1. Application Workflow
The application follows the following logic:
1 ) Check the first frame.
2 ) Check the frames entered later, and identify the pedestrians in the scene through the background splitter from the beginning of the scene.
3 ) Establish an ROI for each pedestrian and use Kalman/CAMShift to track the pedestrian ID .
4 ) Check if there is a pedestrian entering the scene in the next frame.
2 , functional programming and object-oriented programming
Functional programming is a programming paradigm ( paradigm ), many languages ​​are functional programming, they use the program as an estimated mathematical function, allowing the function to return a function, allowing the function as a parameter of another function . The advantage of functional programming is not only what it can do, but also what it can avoid, or whether it avoids side-effects and state changes.
3 , the program

"""
__author__ = "joe minichino"
__copyright__ = "property of mankind."
__license__ = "MIT"
__version__ = "0.0.1"
__maintainer__ = "Joe Minichino"
__email__ = "joe.minichino@gmail.com"
__status__ = "Development"

import cv2
import numpy as np
import os.path as path
import argparse

parser = argparse.ArgumentParser()
parser.add_argument("-a", "--algorithm",
    help = "m (or nothing) for meanShift and c for camshift")
args = vars(parser.parse_args())

def center(points):
    """calculates centroid of a given matrix"""
    x = (points[0][0] + points[1][0] + points[2][0] + points[3][0]) / 4
    y = (points[0][1] + points[1][1] + points[2][1] + points[3][1]) / 4
    return np.array([np.float32(x), np.float32(y)], np.float32)

font = cv2.FONT_HERSHEY_SIMPLEX

class Pedestrian():
  """Pedestrian class

  each pedestrian is composed of a ROI, an ID and a Kalman filter
  so we create a Pedestrian class to hold the object state
  """
  def __init__(self, id, frame, track_window):
    """init the pedestrian object with track window coordinates"""
    # set up the roi
    self.id = int(id)
    x,y,w,h = track_window
    self.track_window = track_window
    self.roi = cv2.cvtColor(frame[y:y+h, x:x+w], cv2.COLOR_BGR2HSV)
    roi_hist = cv2.calcHist([self.roi], [0], None, [16], [0, 180])
    self.roi_hist = cv2.normalize(roi_hist, roi_hist, 0, 255, cv2.NORM_MINMAX)

    # set up the kalman
    self.kalman = cv2.KalmanFilter(4,2)
    self.kalman.measurementMatrix = np.array([[1,0,0,0],[0,1,0,0]],np.float32)
    self.kalman.transitionMatrix = np.array([[1,0,1,0],[0,1,0,1],[0,0,1,0],[0,0,0,1]],np.float32)
    self.kalman.processNoiseCov = np.array([[1,0,0,0],[0,1,0,0],[0,0,1,0],[0,0,0,1]],np.float32) * 0.03
    self.measurement = np.array((2,1), np.float32)
    self.prediction = np.zeros((2,1), np.float32)
    self.term_crit = ( cv2.TERM_CRITERIA_EPS | cv2.TERM_CRITERIA_COUNT, 10, 1 )
    self.center = None
    self.update(frame)

  def __del__(self):
    print "Pedestrian %d destroyed" % self.id

  def update(self, frame):
    # print "updating %d " % self.id
    hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)
    back_project = cv2.calcBackProject([hsv],[0], self.roi_hist,[0,180],1)

    if args.get("algorithm") == "c":
      ret, self.track_window = cv2.CamShift(back_project, self.track_window, self.term_crit)
      pts = cv2.boxPoints(ret)
      pts = np.int0(pts)
      self.center = center(pts)
      cv2.polylines(frame,[pts],True, 255,1)

    if not args.get("algorithm") or args.get("algorithm") == "m":
      ret, self.track_window = cv2.meanShift(back_project, self.track_window, self.term_crit)
      x,y,w,h = self.track_window
      self.center = center([[x,y],[x+w, y],[x,y+h],[x+w, y+h]])  
      cv2.rectangle(frame, (x,y), (x+w, y+h), (255, 255, 0), 2)

    self.kalman.correct(self.center)
    prediction = self.kalman.predict()
    cv2.circle(frame, (int(prediction[0]), int(prediction[1])), 4, (255, 0, 0), -1)
    # fake shadow
    cv2.putText(frame, "ID: %d -> %s" % (self.id, self.center), (11, (self.id + 1) * 25 + 1),
        font, 0.6,
        (0, 0, 0),
        1,
        cv2.LINE_AA)
    # actual info
    cv2.putText(frame, "ID: %d -> %s" % (self.id, self.center), (10, (self.id + 1) * 25),
        font, 0.6,
        (0, 255, 0),
        1,
        cv2.LINE_AA)

def main():
  # camera = cv2.VideoCapture(path.join(path.dirname(__file__), "traffic.flv"))
  camera = cv2.VideoCapture(path.join(path.dirname(__file__), "768x576.avi"))
  # camera = cv2.VideoCapture(path.join(path.dirname(__file__), "..", "movie.mpg"))
  # camera = cv2.VideoCapture(0)
  history = 20
  # KNN background subtractor
  bs = cv2.createBackgroundSubtractorKNN()

  # MOG subtractor
  # bs = cv2.bgsegm.createBackgroundSubtractorMOG(history = history)
  # bs.setHistory(history)

  # GMG
  # bs = cv2.bgsegm.createBackgroundSubtractorGMG(initializationFrames = history)

  cv2.namedWindow("surveillance")
  pedestrians = {}
  firstFrame = True
  frames = 0
  fourcc = cv2.VideoWriter_fourcc(*'XVID')
  out = cv2.VideoWriter('output.avi',fourcc, 20.0, (640,480))
  while True:
    print " -------------------- FRAME %d --------------------" % frames
    grabbed, frame = camera.read()
    if (grabbed is False):
      print "failed to grab frame."
      break

    fgmask = bs.apply(frame)

    # this is just to let the background subtractor build a bit of history
    if frames < history:
      frames += 1
      continue


    th = cv2.threshold(fgmask.copy(), 127, 255, cv2.THRESH_BINARY)[1]
    th = cv2.erode(th, cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (3,3)), iterations = 2)
    dilated = cv2.dilate(th, cv2.getStructuringElement(cv2.MORPH_ELLIPSE, (8,3)), iterations = 2)
    image, contours, hier = cv2.findContours(dilated, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

    counter = 0
    for c in contours:
      if cv2.contourArea(c) > 500:
        (x,y,w,h) = cv2.boundingRect(c)
        cv2.rectangle(frame, (x,y), (x+w, y+h), (0, 255, 0), 1)
        # only create pedestrians in the first frame, then just follow the ones you have
        if firstFrame is True:
          pedestrians[counter] = Pedestrian(counter, frame, (x,y,w,h))
        counter += 1


    for i, p in pedestrians.iteritems():
      p.update(frame)

    firstFrame = False
    frames += 1

    cv2.imshow("surveillance", frame)
    out.write(frame)
    if cv2.waitKey(110) & 0xff == 27:
        break
  out.release()
  camera.release()

if __name__ == "__main__":
  main()
---
