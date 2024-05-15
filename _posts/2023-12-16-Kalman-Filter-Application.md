---
title: Project - Unscented Kalman Filter Application 
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

In mathematical terms, the UKF captures the mean and covariance of the state distribution more accurately by considering terms beyond the first-order linear approximation:

$$\begin{align*}
\chi_t^0 & = x_t \\
\chi_t^i & = x_t + (\sqrt{(n+\lambda)P_t})_i, \quad i=1,2,\ldots,n \\
\chi_t^i & = x_t - (\sqrt{(n+\lambda)P_t})_{i-n}, \quad i=n+1, n+2, \ldots, 2n
\end{align*}$$

$$\hat{\chi}_{t+1}^i = f(\chi_t^i)$$

The update step of the UKF similarly generates sigma points for measurements, predicts expected measurements using the measurement model, and updates the state estimate based on the actual measurements. The UKF combines the information from the prediction and update steps to provide an accurate and robust estimate of the state in the presence of nonlinearities and uncertainty

Unscented Kalman filters not only estimate the state but also provide an estimate of the uncertainty (covariance) associated with that state estimate. Measurement data is used to update this covariance, reflecting the increasing or decreasing confidence in the state estimate. This information is valuable for decision-making and assessing the reliability of the filter's output.

$$K_{t+1} = P_{xz} (P_{zz})^{-1}$$
$$x_{t+1} = \hat{x}_{t+1} + K_{t+1} (z_{t+1} - \hat{z}_{t+1})$$
$$P_{t+1} = \hat{P}_{t+1} - K_{t+1} P_{zz} K_{t+1}^T$$

### For implementing the unscented kalman filter, I assume: 
1. The state X is in gaussian distribution in 3 dimensions. 
2. The control error R ~ N (0, Cov_R)
3. The measurement error meets Q~N (0, Cov_Q)
4. k-1 state the X posterior mean and covariance matrix Miu_X_k-1 and Cov_x_k-1
5. the real measurement value z_k in state k

Firstly, I calculate the predicted trajectory based on the Odometry data, then I pick up the points matched with the measure data time. I used those matched predicted trajectory points to calculate the corresponding measurement values Z_bar, then I input those values into whole algorithm and make estimations on the control and measurement covariance matrix R and Q

![Desktop View](/project_images/SLAM/corrected_trajectory_q0.01.png){: width="372" height="189" }
_Q=0.01_

![Desktop View](/project_images/SLAM/corrected_trajectory_q0.5.png){: width="372" height="189" }
_Q=0.5_

The measurement error has a great impact on my filter path. once the q is decreasing, the plot would become zia-zagging, and once I increase the Q, the path would become smoother. I think that is reasonable, since the Q decides the noise level in the measurement level. Since we do not have the real value Q, once we set the noise level higher, which means the full filter will believe the measurement data less, and the trajectory will be smoother like the estimated trajectory. Once the noise level of Q decrease, the filter believes the measurement data more. Since the measurement data is capatured by different cameras, thus the positions could shift.

# Summary

The motion model performs well in ideal environments without any frictions, and it performs poorly  in real environments if only motion model is used in path estimations. Real-world systems are subject to various sources of error, noise, and uncertainty. Measurement data reflects the actual, observed behavior of the system, but it is often corrupted by noise. Kalman filters use this noisy measurement data to correct and refine the system's state estimate. By continuously updating the state estimate with new measurements, the filter reduces the impact of noise and provides a more accurate and stable estimate.

## Github Link:

https://github.com/haodong0518/Kalman-Filter/tree/main