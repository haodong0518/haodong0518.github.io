---
title: Capstone Project - Motor Position and Velocity Sensor Design for GE Aviation
author: Haodong Wang
date: 2023-05-10 14:10:00 +0800
categories: [Capstone Project]
tags: [Solidworks, Labview]
render_with_liquid: false
image:
  path: /project_images/Motor_sensor.png
  alt: Sensor Test on Milling Machine
---


Engine is an important component in human lives, including space exploration and daily traveling. With the rapid growth of engines, the requirement for components related to engines increases significantly. NASA recently selected GE for a research partnership to focus on developing a hybrid electric system for the Electrified Powertrain Flight Demonstration (EPFD) program. A modified Saab 340B with two CT7-9B turboprop engines was selected as the initial testbed for this project. One of the most important components of this project is an advanced sensor for providing the shaft angular velocity and position. This data is used to optimize an electric motor and other electrical components in the system. It needs to select the best suitable sensor for this project based on the weight, cost, performance in harsh environments, and reliability requirements. 

In the first semester research was done on all kinds of sensors, including Inertial Measurement Units (IMU), Rotary Variable Differential Transformers (RDVT), tachometers, resolvers, and encoders. The resolver was selected after comparing the sensors’ performance in accuracy, endurance in harsh environments, cost, reliability, and weight. 

![Desktop View](/project_images/capstone_project/Motor_Sensor1.png){: width="972" height="589" }
_decision matrix for selecting the sensor_

A decision matrix was used to select the sensor. This table shows the decision matrix in detail. In this table, several types of sensors are listed, and each of these sensors is evaluated based on the design criteria. The weights and the criteria of the decision matrix are provided by GE Aviation. The scale of the sensors is from 1 to 3. Three-point means the sensor is most compliant with the requirements, while one-point means the sensor is the least compliant. Based on the decision matrix, the resolver was chosen. 

![Desktop View](/project_images/capstone_project/circuit_resolver.png){: width="972" height="589" }
_Circuit in the electric resolver_

![Desktop View](/project_images/capstone_project/stator_rotor.png){: width="972" height="589" }
_Stator and Rotor_


The electric resolvers consist of two main components: stator and rotor. In the stator, there are two windings with 90 degrees of displacement from each other, which are sin and cos windings, as shown in Figure. When the rotor starts to rotate within the stator, it induces two AC voltages in sin and cos windings. Thus, the position information of the shaft could be directly calculated by arctan(VsinVcos). The simple design without many electronic elements makes resolvers able to endure a high environmental temperature of up to 220 °C. 


In the second semester, the test is designed, and data is collected from the resolver. 

First of all, the milling machine is used to test the resolver instead of the lathe due to safety and convenience. The milling machine could fix the stator so that our team didn’t need to redesign the holder. In addition, the workstation has extra space to put the computer and connect the resolver. 

![Desktop View](/project_images/Motor_sensor.png){: width="972" height="589" }
_Sensor Test of Milling Machine_


In addition, our team used a photoresistor as a reference to measure the rotation speed. The photoresistor resistance changes with the change of light. A self-designed tachometer is built based on the photoresistor. Dark tape and reflective tapes are attached to the shaft. The resistance will change when the reflective tape on the shaft passes through the photoresistor. With the rotation speed increasing, the resistance frequency will change as well. 

![Desktop View](/project_images/capstone_project/Labview_code.png){: width="972" height="589" }
_Labview Code_


{% include embed/youtube.html id='WpREy1HoCTw' %}



The team used the myDaq measurement device and drew the FFT (Fast Fourier Transform) Plot to monitor the frequency change. Then the rotation speed could be figured out based on the frequency. 

![Desktop View](/project_images/capstone_project/FFT_plot.png){: width="972" height="589" }
_FFT Plot_

## Video

{%include embed/youtube.html id='WpREy1HoCTw'%}


Finally, the data is collected based on two offset change types in the Y and Z axes. Our Team used the digital control in the milling machine to move the stator along the Z axis from -1 mm to 1mm.  Also, the stator moves horizontally from -0.2 mm to 0.1 mm. Based on those two data, our team studied how the error percentage would change with the rotation speed and installation offset changing.
