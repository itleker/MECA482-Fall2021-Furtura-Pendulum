# MECA 482 Furtura Pendulum Final Project
Fall 2021- Group 12

Isaac Leker- James Sandlin- Gaurav Johal- Cole Murdock
## Table of Contents
1. Introduction
2. Modeling
3. Sensor Calibration
4. Controller Design and Simulations
6. Conclusion
7. Appendix: Simulation Code
8. References 

## Introduction
The Furuta Pendulum was invented by Katsuhisa Furuta in 1992 and has since been a widely used tool for teaching the principles of control systems design. The device consists of a motor, which is mounted to a base, that rotates about the vertical axis, and an arm which is free to rotate about the horizontal axis. The arm and motor are connected by a horizontal rod that protrudes from the motor. The goal of this project is to devise a system capable of maintaining the arm balanced upright by controlling the rotation of the motor about the vertical axis.

<p align="center">
  <img width="450" height="600" src="https://user-images.githubusercontent.com/96322953/146626325-e0b81416-4c41-459f-a649-74dc97ff7b37.JPG">
</p>

<p align="center">
Figure 1. Furuta Pendulum (QUANSER QUBE)
</p>

## Modeling

<p align="center">
  <img width="450" height="500" src="https://user-images.githubusercontent.com/96322953/146627318-57c20370-0e2b-4b98-8e8b-4f3797fe0bff.JPG">
</p>

<p align="center">
Table 1. Furuta Pendulum Parameters
</p>

The picture shown in Figure 1 below shows the rotary inverted pendulum model used for the control system design. The rotary arm, which is connected to the motor, has an arm length of Lr and an angle of ___θ___. As the motor rotates in a CCW direction, the angle ___θ___  increases. The moment of inertia of the rotary arm is designated by the variable ___Jr___. The motor turns in the CCW direction whenever the control voltage is greater than ___0___ .

<p align="center">
  <img width="450" height="500" src="https://user-images.githubusercontent.com/96322953/146627046-057f346e-d161-4e1e-a95e-93ed5b53fc6c.JPG">
</p>

<p align="center">
Figure 2. Rotatry Inverted Pendulum Conventions
</p>

## Sensor Calibration
The focus of this project is to design a functional control system, and simulate the results. Since there is no requirement for implementation of physical hardware, there is no sensor, or sensor calibration.

## Contoller Design
__a) Equations of Motions__
  
The Equations of Motion (EOM) section covers the derivation of equations that describe the motion of both the pendulum and rotary arms with respect to the motor voltage.  The full derivation of these equations begins with the Euler-Lagrange equation, seen below in Eq.1.

<p align="center">
  <img width="600" height="100" src="https://user-images.githubusercontent.com/96322953/146627269-19ae27b4-30fa-4a1e-81a8-d030ef7beffd.JPG">
</p>

In this equation, the variables ___qi___ represent what are called generalized coordinates. Because of the nature of our system, it is logical to use polar coordinates. Therefore, the equation for the generalized coordinates is written as 

<p align="center">
  <img width="600" height="75" src="https://user-images.githubusercontent.com/96322953/146628307-b91122d9-7be7-4758-afa2-d34d6dca957a.JPG">
</p>

Where ___𝜃(t)___ is the angle of the rotary arm and ___𝛼(t)___ is the angle of the inverted pendulum (see Figure 1.)  Please note that Eq.2 is presented with respect to time and that from this point on the nomenclature will be simplified to exclude the (t) term in all variables that are with respect to time. That is to say that ___𝜃=𝜃(t)___ and ___𝛼=𝛼(t)___ .

By combining equations 1 and 2, equations 3 and 4 are derived and shown below.___Q1___ and ___Q2___ represent generalized forces acting on each arm.

<p align="center">
  <img width="600" height="75" src="https://user-images.githubusercontent.com/96322953/146628517-7f7f9099-9111-4fd1-9d92-4a7572ef1d2e.JPG">
</p>

<p align="center">
  <img width="600" height="75" src="https://user-images.githubusercontent.com/96322953/146628612-4108893f-74c8-44c9-beb4-d13189ff053a.JPG">
</p>

The Lagrangian of the system is equal to the total kinetic energy of the system minus the total potential energy of the system. It is denoted by the variable L in equations 1-4. The generalized forces acting on each arm ___Q1___, and ___Q2___, are equated to the non-conservative forces acting on each arm. Equations 5 and 6 show this relationship.

<p align="center">
  <img width="600" height="200" src="https://user-images.githubusercontent.com/96322953/146628744-63742d1e-1bb7-4a80-998a-8c242b0a0b3e.JPG">
</p>

The control variable for this system is the voltage input to the servo motor,___Vm___ . As a torque is applied to the servo, it is opposed by a viscous damping force from both arms. The viscous damping forces for the rotary and pendulum arms are ___Br___ and ___Bp___, respectively. After completing the process of obtaining the Lagrangian from the kinetic and potential energies and computing the various derivatives necessary to calculate the EOM’s, the nonlinear equations of motion are found for both arms. The EOM for the rotary arm is shown in Eq. 7 and the EOM for the pendulum arm is shown in Eq. 8.

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146628841-5d275b02-fbe6-4083-bafb-f37283810320.JPG">
</p>

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146629002-6d0de230-b902-48b2-bcd9-f147985cf04c.JPG">
</p>

The torque provided by the servo motor is applied at the base of the motor itself. Eq.9, shown below, describes the torque in terms of the servo motor input voltage Vm, among others.

<p align="center">
  <img width="600" height="100" src="https://user-images.githubusercontent.com/96322953/146629043-2daea252-52ea-40e3-988f-8748f3de9346.JPG">
</p>

The typical form of an EOM is shown in Eq.10, where ___Tau1___ is the scale value of torque applied to the rotary arm via the servo motor, ___g(x)___ describes the gravitational function affecting the system, bis the damping coefficient, and ___J___ is the moment of inertia of the system.

<p align="center">
  <img width="600" height="75" src="https://user-images.githubusercontent.com/96322953/146629223-6505ce85-c257-4795-92b6-b3e2c0f8c9b5.JPG">
</p>

Eq. 10 is used to generalize the coordinate vector q into the matrix form seen in Eq.11 below,

<p align="center">
  <img width="600" height="75" src="https://user-images.githubusercontent.com/96322953/146629250-7d504119-25da-4f25-a670-ff61d370181a.JPG">
</p>

where the inertial matrix is represented by ___D___, the damping matrix is represented by ___C___, the gravitational vector is represented by ___g(q)___, and the applied torque is represented by ___Tau___ .

Finally, the nonlinear EOM’s shown in Eq.7 and Eq.8 can be placed into the matrix form derived above in Eq. 11.

__b) Linearization__
  
In order to linearize the EOM’s for both arms, Eq. 10 is used,

<p align="center">
  <img width="800" height="100" src="https://user-images.githubusercontent.com/96322953/146629575-2ff3a70c-4051-428c-bcf3-f3edb032ee90.JPG">
</p>

where

<p align="center">
  <img width="200" height="100" src="https://user-images.githubusercontent.com/96322953/146629628-2699b908-904c-4837-8290-1b4d6123d5aa.JPG">
</p>

and

<p align="center">
  <img width="200" height="100" src="https://user-images.githubusercontent.com/96322953/146629654-33972d41-d5c0-4163-bf8f-a975db7971fb.JPG">
</p>

__c) Linear State Space__
In the equations for linear state space provided below, ___A___ , ___B___ , ___C___ and ___D___ denote the state space matrices while x denotes the state, and u denotes the control input to the system.

<p align="center">
  <img width="1000" height="100" src="https://user-images.githubusercontent.com/96322953/146630002-f2b52382-d373-4808-933c-b442f858b2e7.JPG">
</p>

The state of the rotary pendulum system then becomes

<p align="center">
  <img width="800" height="100" src="https://user-images.githubusercontent.com/96322953/146630080-efc18948-2f84-4b6e-872c-734cab304cb1.JPG">
</p>

And the output of the system becomes

<p align="center">
  <img width="800" height="100" src="https://user-images.githubusercontent.com/96322953/146630114-075e3821-4ba7-4e21-bc6a-7758fcb2b624.JPG">
</p>

Since only the positions of the servo and the angle of the arms are taken into account in terms of measured variables, the ___C___ and ___D___ matrices corresponding to the output equation are as follows:

<p align="center">
  <img width="700" height="200" src="https://user-images.githubusercontent.com/96322953/146630171-cd0eb666-1025-4509-941d-4ce1e52a8012.JPG">
</p>

By taking the derivatives and filtering the results through a high-pass filter using the digital controller the velocities of both the servo and pendulum can be found.

__d) Linearization of EOM__
For the linearization of Eq.7 and Eq.8, the initial conditions of all the variables are set to equal 0. Under these conditions, the linearized equations Eq.19 and Eq. 20 are derived.

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146630290-241b9ceb-5ffc-4837-bc7c-3a71ad484d60.JPG">
</p>

The following equations display the matrix and determinant needed to calculate the angular acceleration of the rotary and pendulum arm. 

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146630357-e9b0778c-7f59-4aee-9053-9bc50ca84b6b.JPG">
</p>

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146630476-65f73d46-3a66-4d3a-86b7-cc9b41904422.JPG">
</p>

As aforementioned, the above equations are used to calculate the angular accelerations of both arms. These are shown in Eq. 23 and Eq.24 below.

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146630631-db78a98a-f91b-4ef0-b1af-f18fa2c54379.JPG">
</p>

By substituting x3 in for  and x4 in for  into the above equations, we get the following,

<p align="center">
  <img width="800" height="200" src="https://user-images.githubusercontent.com/96322953/146630661-31f40b5c-72d6-4405-bf81-6e05b3332d98.JPG">
</p>

Finally, the matrices A and B from the state space Eq. __X__ is shown below in Eq.27.

<p align="center">
  <img width="800" height="400" src="https://user-images.githubusercontent.com/96322953/146630726-7444538d-d4d3-44e6-8cd1-0c76f339f3e2.JPG">
</p>

## Simulations

<p align="center">
  <img width="800" height="400" src="https://user-images.githubusercontent.com/96322953/146632877-f98d8a0f-a87d-4d41-b499-9345623f2d9f.png">
</p>

<p align="center">
  <img width="800" height="400" src="https://user-images.githubusercontent.com/96322953/146632913-f0a993d6-1c65-456f-891c-d9550b6ddce2.png">
</p>

## Conclusion
The goal of this project was to create a control model that was designed to drive the Furuta Pendulum system. Ideally, the controller designed would be capable of driving the servo motor of the system to keep the pendulum arm balanced. This was accomplished by linearizing the equations of motion derived from the Euler-Lagrange equation. The linearized equations were then represented in state space and moved to a simulation in matlab.

## Appendix: Simulation Code
<p align="center">
  <img width="1000" height="800" src="https://user-images.githubusercontent.com/96322953/146630827-cbe62ee6-01f7-4f24-b8f4-85e46be2c5b8.JPG">
</p>

## Refernces
[1] Wikipedia, Furuta Pendulum, Retrieved by Jan., 27, 2020 from https://en.wikipedia.org/wiki/Furuta_pendulum

[2] Quanser, Rotary Inverted Pendulum, Retrieved by Jan, 27, 2020 from https://www.quanser.com/products/rotary-inverted-pendulum/
 
[3] Control System Tutorials for MATLAB and Simulink, Retrieved by Jan, 27, 2020 from http://ctms.engin.umich.edu/CTMS/index.php?example=InvertedPendulum§ion=SystemModelig 

[4] Kildare, R., Hansen E., Leon, E., PID Control of Furuta Pendulum, Control System Design Project Fall 2019 
