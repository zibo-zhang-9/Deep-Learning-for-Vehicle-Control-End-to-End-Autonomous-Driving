# Deep Learning for Vehicle Control (End-to-End Autonomous Driving)

![Research](https://img.shields.io/badge/Research-Autonomous_Driving-red)
![Field](https://img.shields.io/badge/Field-Machine_Learning-blue)
![Topic](https://img.shields.io/badge/Topic-Control-green)
![Application](https://img.shields.io/badge/Application-Simulation-orange)

This project presents the design and optimization of an **end-to-end learning-based vehicle control system**, where a neural network directly maps **vehicle states and reference trajectories to control commands**.

The objective is to learn a control strategy that enables **stable trajectory tracking** in a simulated autonomous driving environment.

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

Traditional vehicle control relies on model-based approaches such as Proportional–Integral–Derivative (PID) control or Model Predictive Control (MPC).

In contrast, this project explores a data-driven alternative, where a neural network learns the control strategy directly from data. Compared to classical control methods such as PID or MPC, learning-based approaches do not require explicit system modeling, can capture complex nonlinear dynamics, and are capable of adapting to data-driven behaviors [A]. 

Learning vehicle control from data is inherently challenging, as the system must remain stable over time, errors tend to accumulate sequentially, and the underlying dynamics are highly nonlinear and strongly coupled. The problem is formulated as a supervised learning task, where:

- Input: **vehicle states (position, velocity, orientation)** and **reference trajectory**
- Output: **control commands (steering angle and acceleration command)**

The objective is to approximate a mapping: (state, trajectory) → control, which enables **accurate and stable trajectory tracking**.

---

# Processing Pipeline

The overall workflow of the system can be summarized as:

Dataset → Preprocessing → Neural Network Model→ Training → Evaluation → Simulation

---

# Model Design

A **Multi-Layer Perceptron (MLP)** is used as the core Neural Network model.

The model is trained to minimize the difference between predicted and target control commands using Mean Squared Error (MSE) as the loss function.

The model is implemented as a fully connected neural network (MLP) with ReLU activations to capture nonlinear relationships between inputs and outputs.  
It produces continuous-valued control commands, making it suitable for regression-based control tasks.

At the core of the system, the model learns a direct mapping:

```
Vehicle State + Reference Trajectory
   ↓
Neural Network Model (MLP)
   ↓
Control Commands (steering, acceleration)
   ↓
Simulation Environment
```
---

# Training Workflow of the model

## Dataset Processing

The dataset is split into training, validation, and test sets to ensure proper evaluation.
All input features are normalized to improve training stability and convergence.
Each sample is constructed as an input-output pair, where vehicle states and reference trajectories are mapped to control commands.

Example trajectories from the training dataset are shown below:

![trajectories](media/trajectories.png)

## Experimental Methodology

To improve model performance, a systematic experimental methodology was designed. It involves controlled variable analysis and structured hyperparameter exploration.

### Learning Rate Stabilization

To balance convergence speed and stability:

- Fixed learning rates: 1e-3, 1e-4  
- Adaptive scheduling: ReduceLROnPlateau  

### Network Depth Exploration

- Depth range: 1–10 layers  
- Fixed width during experiments

Observation:

- Deeper networks → faster convergence  
- Too deep → instability and degraded performance  

### Network Width Exploration

- Width range: 32–256 neurons

Observation:

- Small models → underfitting  
- Large models → overfitting and unstable training

### Architecture Optimization (Grid Search)

To reduce search complexity, a two-stage grid search was applied:

- Stage 1: optimize early layers  
- Stage 2: refine deeper layers  

## Overfitting Mitigation

Overfitting was identified when validation loss increased while training loss decreased.

To address this issue, several techniques were applied:
- early stopping to prevent excessive training
- continuous monitoring of validation performance
- learning rate adjustment to stabilize training dynamics

---

# Experimental Results

## Training Behavior

The training process shows stable convergence and reduced oscillations after tuning.

Training Curves:

![loss](media/loss.png)

This figure shows the evolution of training and validation loss during optimization.
We observe stable convergence and improved generalization after tuning the learning rate.

## Model Comparison

Different architectures were evaluated to study the effect of depth and width.

The following figure compares models using different depths (layer numbers = 1,3,5,10) while keeping neuron width fixed.

![layers](media/layers.png)

It highlights the trade-off between model capacity and training stability:
deeper networks converge faster but may become unstable.

## Final Model Performance

The optimized architecture achieves a strong balance between accuracy and training stability.

As shown in the figure below, larger models (e.g., 256 neurons) can achieve lower loss but exhibit higher variance and reduced stability. In contrast, smaller models are more stable but tend to underfit.

![final_loss](media/final_loss.png)

The selected architecture is a five-layer MLP with the following structure: **64 → 128 → 64 → 128 → 128**.

This architecture achieves low validation loss while maintaining stable training convergence.

This result indicates that a moderately deep and well-structured network is sufficient to capture the control strategy without introducing instability.

## Simulation Results

The trained model was deployed in a simulation environment.

Example of trajectory tracking is shown below:

![simulation](media/simulation.png)

The predicted trajectory closely follows the reference path with limited lateral deviation. The generated control commands are smooth and consistent, without noticeable oscillatory behavior. In particular, the vehicle maintains stable behavior in curved segments.

This indicates that the model successfully learned the underlying control strategy, and is able to capture the coupling between steering and acceleration dynamics.

---

# Conclusion

This project demonstrates how neural networks can be used to learn vehicle control policies in an end-to-end manner.

Through systematic experimentation, we investigated key factors affecting performance, including network architecture, learning rate, and regularization techniques.

A structured optimization process (including grid search and controlled comparisons) allowed us to identify an effective model configuration that achieves stable and accurate trajectory tracking.

The simulation results show that a properly tuned MLP can achieve stable trajectory tracking in simulation, highlighting the potential of learning-based approaches for control tasks.

Although simplified compared to full-scale autonomous driving systems, this project provides practical insights into the challenges of training neural network models, including overfitting, instability, and model selection.

---

# Technologies Used

## Programming

- Python  

## Machine Learning

- PyTorch / TensorFlow

## Tools

- NumPy  
- Matplotlib  

---

# Applications

Potential applications include:

- autonomous driving control  
- learning-based robotics control  
- imitation learning for dynamic systems

---

# References

[A] Guillaume Devineau. Deep learning for multivariate time series : from vehicle control to gesture recognition and generation. Machine Learning. Université Paris sciences et lettres, 2020.


# Appendix: Implementation Details

## Grid Search Visualization
![grid1](media/grid1.png)
![grid2](media/grid2.png)

---

# Author

Zibo Zhang  
PhD in Robotics  
IMT Atlantique / Université Grenoble Alpes

