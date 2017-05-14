# usb_cam-calibration
Steps to calibrate webcam (monocular camera) using the usb_cam package:


Step1: Make a catkin workspace directory to clone the usb_cam package.

$ mkdir -p ~/workspace/src

$ cd ~/workspace/src

{You can use the ~/catkin-ws/src if you already have}

$ git clone https://github.com/bosch-ros-pkg/usb_cam.git


Step2: Build the package at the root of the catkin workspace.

$ cd ..

$ catkin_make


Step3: Install all the dependencies and compiling the driver of camera_calibration.

$ rosdep install camera_calibration
 
{Here T1, T2, T3 are notations for three separate terminals: T1 is ~/workspace, T2 is to roscore, T3 is to run camera_calibration}


Step4: Publish the images from the webcam over ROS.

T1: $ source ~/workspace/devel/setup.bash

T1: $ roscd usb_cam 

T2: $ roscore

T1: $ rosrun usb_cam usb_cam_node

{You can see the images on Rviz by using $ rosrun rviz rviz}


Step5: Check if /usb_cam/image_raw  and /usb_cam/camera_info topics are published over ROS.

T3: $ rostopic list


Step6: Start the calibration by loading the image_raw topic. 
{Here standard 8x6 checkerboard is used to calibrate the webcam}

T3: $ rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.108 image:=/usb_cam/image_raw camera:=/usb_cam
