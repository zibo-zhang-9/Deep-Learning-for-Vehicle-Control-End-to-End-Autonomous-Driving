# Deep Learning for Vehicle Control (End-to-End Autonomous Driving)

![Research](https://img.shields.io/badge/Research-Autonomous_Driving-red)
![Field](https://img.shields.io/badge/Field-Machine_Learning-blue)
![Topic](https://img.shields.io/badge/Topic-Control-green)
![Application](https://img.shields.io/badge/Application-Simulation-orange)

This project presents the design and optimization of an **end-to-end learning-based vehicle control system**, where a neural network directly maps **vehicle states and reference trajectories to control commands**.

The objective is to learn a control policy that enables **stable trajectory tracking** in a simulated autonomous driving environment.

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

In contrast, this project explores a data-driven alternative, where a neural network learns the control strategy directly from data.

The problem is formulated as a supervised learning task, where:

- Input: vehicle states (position, velocity, orientation) + reference trajectory
- Output: control commands (steering angle, acceleration command)

The objective is to approximate a mapping: (state, trajectory) → control, which enables **accurate and stable trajectory tracking**.

---

# System Architecture

The overall workflow of the system can be summarized as:

Dataset → Preprocessing → Neural Network Model→ Training → Evaluation → Simulation

---

# Model Design

A **Multi-Layer Perceptron (MLP)** is used as the core Neural Network model.

The model is trained to minimize the difference between predicted and target control commands using Mean Squared Error (MSE) as the loss function.

The model is implemented as a fully connected neural network (MLP) with ReLU activations to capture nonlinear relationships between inputs and outputs.  
It produces continuous-valued control commands, making it suitable for regression-based control tasks.

At the core of the system, the model learns a direct mapping:

Vehicle State + Reference Trajectory
↓
Neural Network (MLP)
↓
Control Commands (steering, acceleration)
↓
Simulation Environment

---

# Training Pipeline

## Dataset Processing

- Data split: train / validation / test  
- Feature normalization  
- Input-output pairing (state → control)

---

## Experimental Methodology

To improve model performance, a systematic experimental strategy was designed:

### Learning Rate Stabilization
- Fixed learning rate  
- Dynamic scheduling (ReduceLROnPlateau)
Compared different learning rates:
fixed (1e-3, 1e-4)
dynamic scheduling (ReduceLROnPlateau)
Objective: balance convergence speed and stability
### Network Depth Exploration
- Depth: 1–10 layers  
- Width: 32–256 neurons  
Depth range: 1–10 layers
Fixed neuron size during experiment
Observations:
deeper networks → faster convergence
too deep → instability

→ Selected optimal depth: 5 layers

### Network Width Exploration
Width range: 32–256 neurons
Trade-off:
small model → underfitting
large model → unstable & overfitting

→ Selected base width: 64 neurons

### Architecture Optimization (Grid Search)

To avoid exhaustive search cost, a two-stage grid search was applied:
- Grid Search for optimal architecture  

Stage 1: optimize first layers
Stage 2: optimize remaining layers

Example of final optimized 5-layer architecture:

64 → 128 → 64 → 128 → 128 → output



---

## Overfitting Mitigation

Overfitting was observed when the training loss continued to decrease while the validation loss started to increase.

To address this issue, several techniques were applied:
- early stopping to prevent excessive training
- continuous monitoring of validation performance
- learning rate adjustment to stabilize training dynamics

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

