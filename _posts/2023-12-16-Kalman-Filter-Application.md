---
title: Project - Kalman Filter Application 
author: Haodong Wang
date: 2023-12-16 14:10:00 +0800
categories: [Project,Kalman Filter]
tags: [Python]
render_with_liquid: false
image:
  path: /project_images/slam.png
  alt: UTIAS Multi-Robot Cooperative Localization and Mapping
math: true
---

## Dataset:  
http://asrl.utias.utoronto.ca/datasets/mrclam/index.html#Summary

# Summary

This 2d indoor dataset collection consists of 9 individual datasets. Each dataset contains odometry and (range and bearing) measurement data from 5 robots, as well as accurate groundtruth data for all robot poses and (15) landmark positions. The dataset is intended for studying the problems of cooperative localization (with only a team robots), cooperative localization with a known map, and cooperative simultaneous localization and mapping (SLAM).

# Robot

Each robot and landmark is uniquely identified by a barcode with predefined dimensions. The robots use their cameras, which capture images at a 960×720 resolution, to detect these barcodes. The images are rectified and analyzed to identify the barcodes, from which the identification number, range, and bearing to each barcode are determined. The cameras are mounted on the robots in alignment with their body frames.

![Desktop View](/project_images/SLAM/SLAM_Robot.png){: width="372" height="189" }

# Odometry

Forward velocity commands along the robot's x-axis, v, and angular velocity commands (rotations about the robot's z-axis following the right-hand rule), ω, are recorded as odometry data at an average rate of 67Hz.


# Groundtruth

A 10-camera Vicon motion capture system provides the groundtruth pose (x,y,θ) for each robot and groundtruth position (x,y) for each landmark at 100Hz with accuracy on the order of 1×10-3m. The reference frame used by Vicon serves also as the inertial reference frame in the datasets.

# Mathematics

When given the v, w, delta_t in state k-1, how to find its position in next state k.

$$
\begin{equation}
  \ V_{kx} =V_{k}*cos(\theta_{k-1}+\omega*(t_{k}-t_{k-1}))
  \label{eq:series1}
\end{equation}
$$

$$
\begin{equation}
  \ V_{ky} =V_{k}*sin(\theta_{k-1}+\omega*(t_{k}-t_{k-1})) 
  \label{eq:series2}
\end{equation}
$$

$$
\begin{equation}
  \ P_{x} = \int_{k-1}^{k} V_{k}*cos(\theta_{k-1} + w*(t - t_{k-1})) \,dt = \frac{V_{k}*(sin(\theta_{k-1}+w*\delta_{t})-sin(\theta_{k-1}))}{w} 
  \label{eq:series3}
\end{equation}
$$

$$
\begin{equation}
  \ P_{y} =\int_{k-1}^{k} V_{k}*sin(\theta_{k-1} + w*(t - t_{k-1})) \,dt = \frac{V_{k}*(-cos(\theta_{k-1}+w*\delta_{t})+cos(\theta_{k-1}))}{w} 
  \label{eq:series4}
\end{equation}
$$

$$
\begin{equation}
  \ X_{k} = [t , v, w]^{T}
  \label{eq:series5}
\end{equation}
$$

$$
\begin{equation}
  \ Y_k = [t,P_x, P_y, \theta]^{T }
  \label{eq:series6}
\end{equation}
$$

 I use the X to represent the inputs and Y to represent the outputs in \eqref{eq:series5} and \eqref{eq:series6}. 

![Desktop View](/project_images/SLAM/Estimated%20Trajectory.png){: width="372" height="189" }

The estimated  path distract a lot from the groundtruth path, this is probably caused by control errors, the ground frictions and odometry data. 

![Desktop View](/project_images/SLAM/UKF_Algorithm.png){: width="372" height="189" }

### For implementing the unscented kalman filter, I assume: 
1. The state X is in gaussian distribution in 3 dimensions. 
2. The control error R ~ N (0, Cov_R)
3. The measurement error meets Q~N (0, Cov_Q)
4. k-1 state the X posterior mean and covariance matrix Miu_X_k-1 and Cov_x_k-1
5. the real measurement value z_k in state k

![Desktop View](/project_images/SLAM/corrected_trajectory_q0.01.png){: width="372" height="189" }

![Desktop View](/project_images/SLAM/corrected_trajectory_q0.5.png){: width="372" height="189" }



## Github Link:

https://github.com/haodong0518/Kalman-Filter/tree/main