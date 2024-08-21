---
title: "Visual-Inertial SLAM"
excerpt: "The primary objective of this project was to develop a visual-inertial simultaneous localization and mapping (SLAM) system using an extended Kalman filter (EKF). I utilized synchronized measurements from an inertial measurement unit (IMU) and a stereo camera, alongside the intrinsic camera calibration and the extrinsic calibration between the two sensors. The approach began with the implementation of the prediction step of the EKF to estimate motion and trajectory. Following this, I implemented the update step of the EKF to refine the initial estimates of landmark locations. Finally, I integrated both steps to achieve a fully functional VI-SLAM system using the EKF.<br/><img src='/images/10_3.png' width='500' height='300'>"
collection: portfolio
---
[Full Report](/files/Project_3_ECE_276A.pdf)

*Full code can be provided upon request*


## Introduction
In robotics, enabling systems to perceive and understand their environment accurately is critical for autonomous operation. This project explores visual-inertial simultaneous localization and mapping (VI-SLAM), which integrates visual data from a stereo camera and inertial measurements from an IMU. This combination offers a robust solution to SLAM by utilizing the complementary strengths of visual and inertial data: visual data provides detailed environmental information, while inertial data offers high-rate motion information. The project implements an extended Kalman filter (EKF) based VI-SLAM system, leveraging synchronized IMU measurements and visual feature data to update the robot's position and orientation while constructing and refining a map of the environment.

## Problem Formulation

### What We Have
The project relies on various data inputs:
- **IMU Data:** Includes linear and angular velocities in the IMU's body frame.
- **Visual Feature Measurements:** Pixel coordinates of detected features from the stereo camera, with precomputed correspondences.
- **Time Stamps:** Unix timestamps for each set of measurements.
- **Intrinsic Calibration:** Camera calibration matrix and stereo baseline.
- **Extrinsic Calibration:** Transformation between the IMU and the left camera frame.

### Localization
Localization is achieved using an EKF prediction step, where the robot's state is updated based on IMU data. The process involves:
- **State Update:** Using the exponential map of the twist in the robot's body frame to update the pose.
- **Covariance Update:** Adjusting the covariance to account for uncertainty in the robot's motion.

### Mapping
Mapping involves updating the positions of environmental landmarks using visual observations and EKF updates. The key steps include:
- **Predicted Observation:** Calculating predicted observations for each landmark.
- **Jacobian Calculation:** Deriving the Jacobian of the predicted observation with respect to the map features.
- **EKF Update:** Refining the map estimates using the Kalman gain and updating the landmark positions.

### SLAM
SLAM combines localization and mapping by integrating the trajectory prediction and landmark update processes. This involves:
- **Landmark Prediction:** Triangulating the position of landmarks based on stereo camera data.
- **Pose Update:** Refining the robot's pose using new visual observations and updating the covariance matrix.

## Technical Approach

### IMU Localization via EKF Prediction
IMU data is used to predict the robot's pose and uncertainty over time through:
- **State Prediction:** Updating the robot's pose using the exponential map.
- **Covariance Prediction:** Updating the covariance matrix to reflect the uncertainty in the motion model.

### Landmark Mapping via EKF Update
Landmarks are mapped by triangulating their positions using stereo images and updating these positions with EKF:
- **Observation Processing:** Filtering valid observations from the stereo images.
- **Triangulation:** Converting pixel coordinates to 3D world coordinates.
- **Map Update:** Refining the global map of landmarks with new observations.

### Visual-Inertial SLAM
VI-SLAM integrates IMU localization and landmark mapping, iteratively refining both the robot's trajectory and the map:
- **Motion Model Update:** Updating the robot's pose based on IMU data.
- **Landmark Observation and Update:** Triangulating and updating landmark positions using stereo image data.
- **EKF Update:** Applying the EKF update to refine the state estimates and covariance matrix.

## Results

### Trajectory Estimate and Landmark Locations
- **Figure 1:** Initial trajectory estimate using the EKF prediction.
    ![trajectory](/images/10_1.png)
- **Figure 2:** Landmark initializations versus updated locations after running EKF.
    ![landmark init](/images/10_2.png)
- **Figure 3:** Results of VI-SLAM showing before and after for both trajectory and landmark locations for one noise setting.
    ![ekf](/images/10_3.png)


## Conclusion
The project successfully demonstrated the implementation of VI-SLAM using IMU and stereo camera data, with EKF providing accurate localization and mapping in an unknown environment. The results highlight the importance of sensor noise modeling, as the SLAM process is sensitive to the assumed noise levels. This study underscores the potential of EKF-based VI-SLAM in advancing autonomous robotic navigation and points to future research opportunities in optimizing sensor noise models to further improve the robustness and accuracy of SLAM systems.
