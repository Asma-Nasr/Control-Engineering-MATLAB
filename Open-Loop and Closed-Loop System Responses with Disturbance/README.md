# Open-Loop and Closed-Loop System Responses with Disturbance

## Overview
This repository contains MATLAB code for simulating the response of a control system to both a step input and a disturbed input. A PID controller is implemented to analyze the system's behavior under disturbance.

## Code Explanation

### 1. System Definition
The system is defined using a transfer function:
```matlab
num = [1];
den = [1, 3, 2];
sys = tf(num, den);
```
Numerator: num represents the system's numerator coefficients.
Denominator: den represents the system's denominator coefficients.
### 2. Step Response
A time vector is created, and the step response of the system is computed:
```matlab
t = 0:0.01:10; % Time vector
[y, t] = step(sys, t);
```
### 3. Disturbance
A sinusoidal disturbance is defined:
```matlab
disturbance = 0.1 * sin(2 * pi * 0.5 * t);
```
### 4. Closed-Loop System
A PID controller is designed, and the closed-loop system is created:
```matlab
C = pid(1, 1, 0);
sys_closed = feedback(C * sys, 1);
```
### 5. Input Simulation
The total input, including the disturbance, is simulated:
```matlab
u = ones(size(t));
u_disturbed = u + disturbance;
[y_disturbed, t] = lsim(sys_closed, u_disturbed', t);
```
### 6. Results Visualization
The responses are plotted for comparison:
```matlab
figure;
hold on;
plot(t, y, 'b', 'DisplayName', 'Step Response without Disturbance');
plot(t, y_disturbed, 'r', 'DisplayName', 'Response with Disturbance and PID');
title('System Response Comparison');
xlabel('Time (s)');
ylabel('Response');
legend;
grid on;
```
## Requirements
- MATLAB
## How to Run
- Clone the repository:
```bash
git clone https://github.com/Asma-Nasr/Control-Engineering-MATLAB.git
cd Control-Engineering-MATLAB
cd "Open-Loop and Closed-Loop System Responses with Disturbance"
```
## Results
![Results](https://github.com/Asma-Nasr/Control-Engineering-MATLAB/blob/main/Open-Loop%20and%20Closed-Loop%20System%20Responses%20with%20Disturbance/output.png)
