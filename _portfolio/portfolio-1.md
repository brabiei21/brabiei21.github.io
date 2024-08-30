---
title: "Orientation Tracking (Click Here!)"
excerpt: "The objective of the project is to track the orientation of a rigid body given sensor measurements by performing projected gradient descent and to generate a panorama by linking camera readings with rotations based on timestamps.<br/><img src='/images/pano9.png' width='500' height='300'>"
collection: portfolio
---
[Full Report](/files/Project_1_ECE_276A.pdf)

*Full code can be provided upon request*
## Introduction
Robotic autonomy hinges on four core components: localization, planning, mapping, and control. This project focuses on localization, specifically tracking the orientation of a camera equipped with an IMU (Inertial Measurement Unit) over time. The project's goal includes validating this approach using VICON motion capture data as ground truth and creating a 3D panorama from the captured images to further verify the results.

## Problem Formulation

### Orientation Tracking
The objective is to track the orientation of a camera using IMU data. The IMU provides linear acceleration and angular velocity data, which, along with quaternion kinematics, is used to predict the camera's orientation over time. The goal is to estimate the orientation trajectory using a motion model and an observation model that takes gravity into account.

### Panorama
The project also aims to generate a panoramic image by stitching together the camera images based on the estimated orientation. This involves calculating the orientation at each timestamp and using this to align the images correctly.

## Technical Approach

### Sensor Calibration
Before processing the data, it’s essential to calibrate the IMU to correct known biases and errors, such as flipped axes and incorrect angular velocity ordering. The IMU data is adjusted using scale factors and biases derived from sensor datasheets and VICON data. After calibration, both the IMU and VICON data are visualized to ensure accuracy.

- **Figure 1:** IMU Data before Processing.
  ![Pre Processing](/images/IMU_init.png)
- **Figure 2:** IMU Data after Processing.
  ![Post Processing](/images/IMU_final.png)
- **Figure 3:** Euler Angles of VICON.
  ![VICON](/images/VIC.png)

### Orientation Tracking
Orientation tracking is achieved through a cost function that combines the motion model and the observation model. The initial trajectory is estimated, then refined using a constrained gradient descent algorithm. The results are compared against the VICON data to validate the estimates.


  - **Figure 4:** Motion Estimate Vs. VICON (Initial).
  ![Motion Estimate Init](/images/motion_vic_init.png)

  - **Figure 5:** Observation Estimate Vs. Accelerometer (Initial).
  ![Visual Estimate](/images/observation_acc_init.png)

### Panorama
Once the orientation is tracked, the next step is constructing a panoramic image. This involves converting pixel coordinates to spherical coordinates, rotating these according to the estimated orientation, and then mapping them back to an image. The resulting panorama visually represents the camera's field of view over time.

## Results

### Orientation Tracking
The final orientation estimates show a significant improvement after optimization, closely matching the VICON data. However, in some datasets, especially those with an IMU reset glitch, there is an offset in the yaw angle that remains after training.

- **Figure 6:** Motion Estimate Vs. VICON (Final).
  ![Motion Estimate Init](/images/motion_vic_final.png)

- **Figure 7:** Observation Estimate Vs. Accelerometer (Final).
  ![Visual Estimate](/images/observation_acc_final.png)
- **Figure 8:** Loss Curve.
  ![Loss Curve](/images/lost_curve.png)

### Panorama
The generated panoramic image gives a reasonable representation of the captured environment, although some datasets exhibit distortions likely due to camera tilt.
- **Figure 9:** Final Panoramic.
  ![Panorama](/images/pano9.png)

<!-- ## Figures

- **Figure 1:** IMU Data before Processing.
  ![Pre Processing](/images/IMU_init.png)
- **Figure 2:** IMU Data after Processing.
  ![Post Processing](/images/IMU_final.png)
- **Figure 3:** Euler Angles of VICON.
  ![VICON](/images/VIC.png)
- **Figure 4:** Motion Estimate Vs. VICON (Initial).
  ![Motion Estimate Init](/images/motion_vic_init.png)
- **Figure 5:** Motion Estimate Vs. VICON (Final).
  ![Motion Estimate Init](/images/motion_vic_final.png)
- **Figure 6:** Observation Estimate Vs. Accelerometer (Initial).
  ![Visual Estimate](/images/observation_acc_init.png)
- **Figure 7:** Observation Estimate Vs. Accelerometer (Final).
  ![Visual Estimate](/images/observation_acc_final.png)
- **Figure 8:** Loss Curve.
  ![Loss Curve](/images/lost_curve.png)
- **Figure 9:** Final Panoramic.
  ![Panorama](/images/pano9.png) -->
