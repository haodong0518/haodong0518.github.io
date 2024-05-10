---
title: Project - Mecanum Wheels and 5R Robot Arm Simulation
author: Haodong Wang
date: 2024-01-15 14:10:00 +0800
categories: [Project,Simulation]
tags: [Matlab]
render_with_liquid: false
image:
  path: /project_images/robotArm.png
  alt: Mobile Manipulation
---

Github Link:  https://github.com/haodong0518/Mobile-Manipulation

In this capstone project, I developed a software designed to plan a trajectory for the end-effector of the youBot mobile manipulator. This system comprises a mobile base equipped with four mecanum wheels and a 5R robot arm. My task involves implementing odometry to track chassis movement, as well as feedback control to guide the youBot in picking up a block from a specified location, transporting it to a desired destination, and placing it down.

Upon completion, it will generate a comma-separated values (csv) text file. This file will detail the configurations of both the chassis and the arm, including the angles of the four wheels and the state of the gripper (whether open or closed) over time. To evaluate the effectiveness of my trajectory, I will utilize the CoppeliaSim simulator. Specifically, I will employ Scene 6 (CSV Mobile Manipulation youBot) from the CoppeliaSim Introduction wiki page. Prior to executing my solution, I will verify its functionality by testing it with the provided sample csv file.

![Desktop View](/project_images/Mobile_Manipulation/bot_steps.png){: width="972" height="589" .w-50 .left}

