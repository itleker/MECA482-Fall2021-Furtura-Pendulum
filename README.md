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

(![Introduction_Meca_482](https://user-images.githubusercontent.com/96322953/146626325-e0b81416-4c41-459f-a649-74dc97ff7b37.JPG)

## Modeling
The picture shown in Figure 1 below shows the rotary inverted pendulum model used for the control system design. The rotary arm, which is connected to the motor, has an arm length of Lr and an angle of __θ__. As the motor rotates in a CCW direction, the angle __θ__  increases. The moment of inertia of the rotary arm is designated by the variable __Jr__. The motor turns in the CCW direction whenever the control voltage is greater than __0__ .

## Sensor Calibration
