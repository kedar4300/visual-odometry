# Visual Odometry for camera trajectory Tracking
  Using a fisheye lens for Visual Odometry algorithm we aim to recover accurate trajectory of the camera moving in an environment.
  
# Description
  Visual Odometry is a crucial concept in Robotics Perception for estimating the trajectory of the robot (the camera on the robot to be precise).
  With this project we are aiming to use a fisheye lens for Visual Odometry algorithm and to recover accurate trajectory of the camera moving in an environment.
  
  
  ![alt text]( https://github.com/kedar4300/visual-odometry/blob/main/flowchart.png?raw=true)
 # Table of Content:
  - Problem Statement
  - Introduction
  - Theory
  - Results 
  - Credits
  - Reference
  - Conclusion
 
 # Code Setup and Execution:
  - Download the zipped folder and unzip it. 
  - Install the required dependencies using pip 
  - make your current working directory has the requirements.txt file. 
  - Just open the terminal inside the unzipped folder:
    - `pip3 install -r requirements.txt`
 - `Run main.py. `
 - If there are any errors in reading the images. Make sure that the path mentioned in main.py line 11 is correct. 


# Approach and implementation:
- To estimate the 3D motion (translation and rotation) between successive frames in the sequence:
    - Point correspondences between successive frames were found using [SIFT](https://medium.com/data-breach/introduction-to-sift-scale-invariant-feature-transform-65d7f3a72d40) (Scale Invariant Feature Transform) algorithm. (refer to _extract_features()_ function in [main.py](
    - [Fundamental matrix](https://www.robots.ox.ac.uk/~vgg/hzbook/hzbook2/HZepipolar.pdf) (F) was estimated using 8-point algorithm within RANSAC (refer to _fundmntl_mat_from_8_point_ransac()_ function in [main.py]
    - [Essential matrix](https://www2.cs.duke.edu/courses/fall15/compsci527/notes/epipolar-geometry.pdf) (E) was estimated from the fundamental matrix using the camera calibration parameters given. (refer to _calc_essential_matrix()_ function in [main.py]
    - E matrix was decomposed into to translation(T) and rotation(R) matrices to get four possible combinations.
    - Correct R and T were found from testing the depth positivity, i.e. for each of the four solutions depth of all the points was linearly estimated using the cheirality equations. The R and T that gave the maximum number of positive depth values was chosen. 
    - For each frame, the position of the camera center was plotted based on the rotation and translation parameters between successive frames.
- The rotation and translation parameters that were calculated and the plot were compared against the ones calculated using opencv's _cv2.findEssentialMat()_ and _cv2.recoverPose()_ functions.
- To have a better estimate of the R and T parameters, was enhanced to solve for depth and the 3D motion non-linearly using non-linear triangulation (for estimating depth) and non-linear PnP (for estimating R and T).

# Theory
 - Visual Odometry
    - In robotics and computer vision, visual odometry is the process of determining the position and orientation of a robot by analyzing the associated camera images. It has been used in a wide variety of robotic applications, such as on the Mars Exploration Rovers.
 - fisheye lens 
    - A fisheye lens is an ultra wide-angle lens that produces strong visual distortion intended to create a wide panoramic or hemispherical image.
    - Fisheye lenses achieve extremely wide angles of view, well beyond any rectilinear lens.
    - Instead of producing images with straight lines of perspective (rectilinear images)
    - fisheye lenses use a special mapping ("distortion"; for example: equisolid angle, see below), which gives images a characteristic convex non-rectilinear appearance


 
 # Results and Conclusion:
img_rect 1156            |  img_rect 1157
:-------------------------:|:-------------------------:
![](https://...Dark.png)  |  ![](https://...Ocean.png)
![](https://github.com/kedar4300/visual-odometry/blob/main/frame001156.png?raw=true)  |  ![](https://github.com/kedar4300/visual-odometry/blob/main/frame001157.png?raw=true)
Fisheye 1193             | Fisheye  1194
![](https://github.com/kedar4300/visual-odometry/blob/main/frame001193.png?raw=true)  |  ![](https://github.com/kedar4300/visual-odometry/blob/main/frame001194.png?raw=true)
Result 01             | Result 02
![](https://github.com/kedar4300/visual-odometry/blob/main/result1.png?raw=true)  |  ![](https://github.com/kedar4300/visual-odometry/blob/main/result2.png?raw=true)
 
 
 
 # Credits:
 - Yagnesh Devada (BT19ECE122)
 - Mandar Patil  (BT19ECE083)
 - Bhavesh Ugemuge (BT19ECE116)
 - Anup Hujare  (BT19ECE010)
 - Kedar Sonvane (BT19ECE106)
 
 # References:
- [Lecture on Fundamental Matrix](https://www.youtube.com/watch?v=K-j704F6F7Q)
- [Epipolar Geometry](https://web.stanford.edu/class/cs231a/course_notes/03-epipolar-geometry.pdf)
- [Eight point algorithm](http://www.cs.cmu.edu/~16385/s17/Slides/12.4_8Point_Algorithm.pdf)
- [Camera Calibration and Fundamental Matrix Estimation with RANSAC](https://www.cc.gatech.edu/classes/AY2016/cs4476_fall/results/proj3/html/sdai30/index.html)
- [Structure from Motion](https://cmsc426.github.io/sfm/)
