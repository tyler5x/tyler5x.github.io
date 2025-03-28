---
name: 5-DOF Robot Arm
tools: [Inverse Kinematics, Computer Vision, Trajectory Optimization]
image: ../media/armlab/armlab.jpeg
description: A 5-DOF arm that uses computer vision to autonously manipulate objects.
---

# 5-DOF Robot Arm

## Overview
This was the first of two projects done in my Robotic Systems Lab class at the University of Michigan. The goal was to program a
5 degree of freedom robot arm to accomplish manipulation tasks autonomously, including sorting and stacking blocks of different
size, shape, and color. I worked on this project with two other students, and played a key role in developing all of the 
algorithms.

This page gives a brief overview of the steps leading to complete sorting and stacking autonomy. 
View our [full report](../media/armlab/armlab.pdf){:target="_blank"} for more technical detail including our detailed methodolgy
and mathematical derivations.

## Results
Below is a video of the robot autonomously sorting small and large blocks into separate stacks on either side of the arm. The vision
system had to distinguish between the small blocks stacked on top of the larger blocks and the vision, calibration, and kinematics all
needed to be precise to stack the blocks. The stacking worked well on most occasions but not all - there's certainly room for improvement.

<div style="text-align: center;">
    <!-- <iframe src="https://youtu.be/EOz6ubrqf-s" width="800" height="480" frameborder="0" allow="autoplay" allowfullscreen></iframe> -->
    <iframe width="800" height="480" src="https://www.youtube.com/embed/EOz6ubrqf-s" title="Block Stacking" frameborder="0" allow="autoplay" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</div>

## Checkpoints
The milestones for this project were broken down into a series of checkpoints to build up the functionality of the robot arm in
pieces. 

### Checkpoint 1: Teach & Repeat
The goal of the first checkpoint was to teach the robot to repeat actions. We moved the robot to specific positions by hand,
recorded the encoder angles, and then commanded the robot to go to the saved poses. We used a stack to store the positions as
they were added. The recording of poses is on the left and the repeated series of actions is on the right.

<div style="display: flex; gap: 20px; justify-content: center; flex-wrap: wrap;">
    <iframe src="https://drive.google.com/file/d/1mSbzq_doTXEdhY8If-JonnAdE9ZhTwGi/preview" width="400" height="600" allow="autoplay" allowfullscreen></iframe>
    <iframe src="https://drive.google.com/file/d/1NkzLhYUJMnAC0xiov47WnAOlSxNifJpR/preview" width="400" height="600" allow="autoplay" allowfullscreen></iframe>
</div>

<br>

### Checkpoint 2: Camera Calibration & Forward Kinematics
For this checkpoint, we first had to calibrate the camera using april tags. We first used a calibration checkerboard to determine the camera intrinsic
matrix, but chose to use the factory calibration since the manual calibration showed considerable variation between trials. We use four april tags with
known world coordinates and the openCV function solvePNP() to determine the extrinsic matrix. The function takes the list of world points, image points, 
the camera intrinsic matrix, and distortion coefficients as parameters and outputs the rotation vector and translation vector needed to produce the 
extrinsic camera matrix as a homogenous transformation matrix. Additionally, we use a homography transformation to warp the raw camera image to align
with the screen on the GUI. This perspective warp and the world coordinates using the computed transformation matrices are shown in the video below.

<div style="text-align: center;">
    <iframe src="https://drive.google.com/file/d/1b3m27ZaTuy9219F9qpAvSjd2YDo41pyd/preview" width="800" height="480" allow="autoplay" allowfullscreen></iframe>
</div>

<br>

We also used forward kinematics to determine the end effector location in (x,y,z) world coordinates based on the joint angles read by the servo encoders.
The end effector position is calculated using a sequential multiplication of homogenous transformation matrices for each joing, determined using the 
Denavit-Hartenberg (DH) parameter method. 
In the video below, we confirm that the calculated end effector position matches the known world coordinate at the desired points:
(0, 175, 100), (-300, -75, 25), (300, -75, 50), and (300, 325, 10). We achieve good results, with some error occuring since the robot is being manually
moved to approximate locations.

<div style="text-align: center;">
    <iframe src="https://drive.google.com/file/d/1Mr7uu_OmLj1-X_08pPF-n53C87aGKFsj/preview" width="800" height="480" allow="autoplay" allowfullscreen></iframe>
</div>
<br>

### Checkpoint 3: Pick & Place
For this checkpoint, we used inverse kinematics to pick up blocks using user input from the GUI. We convert GUI mouse coordinates to world coordinates using
the perspective transform and extrinsic matrix described previously, and use inverse kinematics to command joing angles to the robot. We simplify the inverse 
kinematics problem by constraining the arm to 3 DOF and then use a numerical solver to solve for a suitable set of joint angles to achieve the desired pose.

<div style="text-align: center;">
    <iframe src="https://drive.google.com/file/d/1ayfPWLI4QZ2ufSywJyTtVa-w3jew3rKG/preview" width="800" height="480" allow="autoplay" allowfullscreen></iframe>
</div>
<br>

We also implemented an OpenCV block detection system that determines the size, color, and position of blocks.

<div style="text-align: center;">
    <iframe src="https://drive.google.com/file/d/1QV2yGgm0XVEmZxN9IDunNJ7ZlSAerCLZ/preview" width="800" height="480" allow="autoplay" allowfullscreen></iframe>
</div>
<br>

