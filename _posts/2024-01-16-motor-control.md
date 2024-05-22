---
title: Project - PID Motor Control Based on PIC32 Board
author: Haodong Wang
date: 2024-01-16 14:10:00 +0800
categories: [Project,Motor_Control]
tags: [c_language]
image:
  path: /project_images/motor_control.jpeg
  alt: Circuit Configurations
---

Github Link: https://github.com/haodong0518/PID-Motor-Control

Background:

Building a smart motor driver for a robot joint that incorporates some of the functionality of an industrial product like the Copley Accelus driver. The drive integrates an amplifier to drive the motor and feedback control for tracking reference position, speed or torque.

This motor drive system can accept a desired motor trajectory, execute that trajectory, and send the actual results back to the computer for plotting.

Components:

## Motor pinout:

![Desktop View](/project_images/motor_control/motor_pins.png){: width="972" height="589" }
_Motor Pins_

- [ ] Pin 1 - Motor +
- [ ] Pin 2 - Motor -
- [ ] Pin 3 - Encoder GND
- [ ] Pin 4 - Encoder B
- [ ] Pin 5 - Encoder 3.3V
- [ ] Pin 6 - Encoder A
The encoder has 96 lines.


## The Raspberry Pi Pico H:
![Desktop View](/project_images/motor_control/pico.png){: width="972" height="589" }
_Pico H_

## Diagram:
![Desktop View](/project_images/motor_control/pid_control.png){: width="972" height="589" }
_PID loop_

![Desktop View](/project_images/motor_control/components.png){: width="972" height="589" }
_Components_

![Desktop View](/project_images/motor_control/hand_draw.png){: width="972" height="589" }
_Hand Drawing Circuit Diagram_

![Desktop View](/project_images/motor_control.jpeg){: width="972" height="589" }

## Results:

Parameters:

Control gains I used:
- [ ] Kp: 2.4 %duty/mA
- [ ] Ki: 0.4 %duty/(mA*s)

Position Control:
- [ ] Kp: 10 mA/deg
- [ ] Ki: 0 mA/(deg*s)
- [ ] Kd: 10 mA*s/deg

Unit:
- [ ] Kp is percent per million amp
- [ ] Ki is percent per million amp per second
- [ ] Kd is degrees per million amp second.

![Desktop View](/project_images/motor_control/Result1.jpg){: width="972" height="589" }
_Red is Desired Trajectory, Blue is the actual Trajectory_

![Desktop View](/project_images/motor_control/Result2.jpg){: width="972" height="589" }
_Red is Desired Trajectory, Blue is the actual Trajectory_