# Deep Learning for Vehicle Control (End-to-End Autonomous Driving)

![Research](https://img.shields.io/badge/Research-Autonomous_Driving-red)
![Field](https://img.shields.io/badge/Field-Machine_Learning-blue)
![Topic](https://img.shields.io/badge/Topic-Control-green)
![Application](https://img.shields.io/badge/Application-Simulation-orange)

This project presents the design and optimization of an **end-to-end learning-based vehicle control system**, where a neural network directly maps **vehicle states and reference trajectories to control commands**.

The goal is to learn a control policy that enables **stable trajectory tracking** in a simulated autonomous driving environment.

This work was conducted at the **Institute for Intelligent Systems and Robotics (ISIR), Sorbonne University**.

---

# Project Highlights

• End-to-end mapping from state → control using neural networks  
• Systematic model optimization via controlled experiments  
• Grid search for architecture tuning  
• Overfitting analysis using validation curves  
• Simulation-based validation of learned control policies  

---

# Overview

Traditional vehicle control relies on model-based approaches such as PID or MPC.

In contrast, this project explores a **data-driven alternative**, where a neural network learns the control policy directly from data.

The system takes as input:

- vehicle states (position, velocity, orientation)
- reference trajectory

and outputs:

- steering angle
- acceleration command

The objective is to enable **accurate and stable trajectory tracking** using learned policies.

---

# System Architecture

The pipeline consists of the following stages:
