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

required: CoppeliaSim Installed

In this capstone project, I developed a software designed to plan a trajectory for the end-effector of the youBot mobile manipulator. This system comprises a mobile base equipped with four mecanum wheels and a 5R robot arm. My task involves implementing odometry to track chassis movement, as well as feedback control to guide the youBot in picking up a block from a specified location, transporting it to a desired destination, and placing it down.

Upon completion, it will generate a comma-separated values (csv) text file. This file will detail the configurations of both the chassis and the arm, including the angles of the four wheels and the state of the gripper (whether open or closed) over time. To evaluate the effectiveness of my trajectory, I will utilize the CoppeliaSim simulator. Specifically, I will employ Scene 6 (CSV Mobile Manipulation youBot) from the CoppeliaSim Introduction wiki page. Prior to executing my solution, I will verify its functionality by testing it with the provided sample csv file.

![Desktop View](/project_images/Mobile_Manipulation/bot_steps.png){: width="372" height="189" }

## CSV Output:

The software will output a CSV file with the youBot's configurations, wheel angles, and gripper state.
This CSV file will be played in CoppeliaSim to simulate the robot’s performance.
CoppeliaSim Setup:

Use Scene 6 (CSV Mobile Manipulation youBot) from the CoppeliaSim Introduction wiki.
Test with the sample CSV file to understand the required solution format.
Physics Simulation:

Utilize CoppeliaSim’s physics engine to simulate interactions between the youBot and the block.
Default to the ODE physics engine, though alternatives like Bullet and MuJoCo are available.
Detailed Requirements

## CSV File Specifications:

Each line represents the youBot’s configuration at a 0.01-second interval.
A line consists of 13 values: 

![Desktop View](/project_images/Mobile_Manipulation/csv_13_values.png){: width="972" height="589" }
_CSV File 13 values for each line_

## Trajectory Segments:

 - [ ] Move the gripper from its initial configuration to above the block (standoff position).
 - [ ] Lower the gripper to grasp the block.
 - [ ] Close the gripper.
 - [ ] Lift the block back to the standoff position.
 - [ ] Move to the standoff position above the final block location.
 - [ ] Lower the block to the final position.
 - [ ] Open the gripper.
 - [ ] Return the gripper to the standoff position.

## Dimensions

![Desktop View](/project_images/Mobile_Manipulation/5R-joint.png){: width="972" height="589" }
_5R Robot Configuration_

![Desktop View](/project_images/Mobile_Manipulation/gripper_tip.png){: width="500" height="300" }
_gripper_

![Desktop View](/project_images/Mobile_Manipulation/mecanum_wheel.png){: width="500" height="300" }
_omnidirectional mobile base_

![Desktop View](/project_images/Mobile_Manipulation/cube_dimension.png){: width="500" height="300" }
_cube dimensions_


## Control and Simulation:

Implement a Jacobian pseudoinverse position controller to follow the reference trajectory.
Perform odometry to track chassis movement. 

## Inputs: 

- Initial block configuration.
- Desired final block configuration.
- Initial youBot configuration.
- Initial reference trajectory for the end-effector.
- Optional: Feedback controller gains.
  
## Outputs:

- A CSV file for CoppeliaSim to simulate the youBot’s task.
- A data file with the end-effector error as a function of time.

## Milestones:

- Milestone 1: Kinematics simulator and CSV output.
- Milestone 2: Reference trajectory generation.
- Milestone 3: Feedforward control.

By following these steps, I created a robust software solution to control the youBot, achieving precise and accurate mobile manipulation in a simulated environment.
