---
layout: post
title: DS3218 SERVO MOTOR SIMULATION
category: blog
description: tttttttttttttt
---

## Introduction 
The main purpose of this project is to simulate the servo motor `DS3218` in Gazebo since the nature of the actuator/controller embeded inside the Gazebo simulator as well as the servo itsef in the real world remain unclear. Thus the project is seperated into three steps. The first stage is the verification of the dynamics of the Gazebo actuator simuator. Typically, the actuator is modeled as a second-order plant. Then, show the same step response in `Matlab` by using the identical parameters(damping and P gain). The second step is to establish the realation between the electrical parameters and mechenical parameters. The last step is to verify the results on the real motor and in the Gazebo simulation.

## Assumptions 
1. Ignore the induction effect between the rotor and the stator.
2. The force factor $K_t$ is identical to the electrical factor $K_e$ in terms of value.
3. 

## Model
### Ignore the static friction
The dynamics equation can be derived from Newton's second law.
$$
J_m \ddot{\theta} + \zeta \dot{\theta} = \tau
$$
where the $J_m$ is the inertia of the load applied on the turning axis, $\zeta$ is known as the damping, and $\tau$ is the torque. Therefore the transfer function becomes:
$$
\frac{\Theta(s)}{{\rm T} (s)}= \frac{1}{J_ms^2 + \zeta s} = \frac{K}{s(\beta s + 1)}
$$
in which
$$
K = \frac{1}{\zeta},\ \ \ \ \  \beta = \frac{J_m}{\zeta}
$$
According to the 
