# Deep Learning for Vehicle Control (End-to-End Autonomous Driving)

![Research](https://img.shields.io/badge/Research-Autonomous_Driving-red)
![Field](https://img.shields.io/badge/Field-Machine_Learning-blue)
![Topic](https://img.shields.io/badge/Topic-Control-green)
![Application](https://img.shields.io/badge/Application-Simulation-orange)

This project presents the design and optimization of an **end-to-end learning-based vehicle control system**, where a neural network directly maps **vehicle states and reference trajectories to control commands**.

The goal is to learn a control policy that enables **stable trajectory tracking** in a simulated autonomous driving environment.

This work was conducted at between the **Institute for Intelligent Systems and Robotics (ISIR), Sorbonne University** and **Mines Paris, PSL University**.

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

In contrast, this project explores a data-driven alternative, where a neural network learns the control policy directly from data.

The problem is formulated as a supervised learning task, where:

- Input: vehicle states (position, velocity, orientation) + reference trajectory
- Output: control commands (steering angle, acceleration command)

The objective is to approximate a mapping: (state, trajectory) → control enabling **accurate and stable trajectory tracking**.

---

# System Architecture

The pipeline consists of the following stages:

Dataset → Preprocessing → Neural Network → Training → Evaluation → Simulation

Illustration:

Vehicle State + Reference Trajectory

↓

Neural Network (MLP)

↓

Control Commands (steering, acceleration)

↓

Simulation Environment


---

# Model Design

A **Multi-Layer Perceptron (MLP)** is used as the core model.

Key characteristics:

- Input: vehicle state + trajectory features  
- Output: continuous control commands  
- Fully connected architecture  

Example optimized architecture:

64 → 128 → 64 → 128 → 128 → output


---

# Training Pipeline

## Dataset Processing

- Data split: train / validation / test  
- Feature normalization  
- Input-output pairing (state → control)

---

## Optimization Strategy

To improve model performance, systematic experiments were conducted:

### Network Structure Exploration

- Depth: 1–10 layers  
- Width: 32–256 neurons  

### Learning Rate Tuning

- Fixed learning rate  
- Dynamic scheduling (ReduceLROnPlateau)

### Model Selection

- Grid Search for optimal architecture  
- Final selected structure: `64-128-64-128-128`

---

## Overfitting Mitigation

Overfitting was detected via:

- divergence between training and validation loss  

Solutions:

- early stopping  
- validation monitoring  

---

# Experimental Results

## Training Behavior

- stable convergence observed  
- reduced validation loss after tuning  

## Simulation Performance

The trained model was deployed in a simulation environment.

Results:

- stable trajectory tracking  
- smooth control output  
- no oscillatory behavior  

---

# Technologies Used

## Programming

- Python  

## Machine Learning

- PyTorch / TensorFlow (depending on your actual stack)

## Tools

- NumPy  
- Matplotlib  

## Simulation

- custom simulation / provided framework  

---

# Applications

Potential applications include:

- autonomous driving control  
- learning-based robotics control  
- imitation learning for dynamic systems  

---

# Limitations & Future Work

- limited generalization to unseen environments  
- no perception module (state is assumed known)  
- future work: integrate perception + RL  

---

# Author

Zibo Zhang  
PhD in Robotics  
IMT Atlantique / Université Grenoble Alpes

