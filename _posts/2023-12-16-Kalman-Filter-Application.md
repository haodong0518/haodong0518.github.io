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

# Mathematics

The mathematics powered by [**MathJax**](https://www.mathjax.org/):

$$
\begin{equation}
  \sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6}
  \label{eq:series}
\end{equation}
$$