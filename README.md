# PID Controlled Ball Balance Platform with FPGA
 
A six-servo, vision-based ball-balancing platform that keeps a ball centered on a tiltable surface using real-time closed-loop control, with the goal of also moving the ball to commanded locations, recovering from disturbances, and following patterns.
 
## Abstract
 
An overhead camera continuously reports the ball's coordinates, an FPGA computes a PID correction and drives servo motors that tilt the platform to push the ball back toward the setpoint, and a Raspberry Pi supervises the system — setting targets, tuning gains, and logging performance. A planned future feature is drawing shapes using the PID control and the ball's coordinates.
 
## How it works
 
The FPGA runs the control loop at a fixed frequency, entirely in hardware with no OS in the loop, so timing stays deterministic regardless of what else is running on the Pi:
 
1. The **camera** picks up and reports the ball's current coordinates.
2. The **FPGA** compares that position to the target setpoint and computes a PID correction.
3. The FPGA converts the correction into **PWM signals** driving the **servo motors**.
4. The servos **tilt the platform**, changing the ball's motion and closing the loop back to the camera.
## Project goals
 
Combine computer vision, FPGA-based PID control, inverse kinematics, and six-servo actuation into one closed-loop system that can:
- Detect the ball's position
- Calculate the required corrective motion
- Center the ball, move it to commanded locations, recover from disturbances, and follow patterns
## Repository structure
 
```
fpga/         FPGA source (PID control, servo interfacing, timing), testbenches, build constraints
pi/           Raspberry Pi software (camera/image processing, communication, logging)
mechanical/   Platform CAD, six-servo mounting, bill of materials
docs/         Block diagrams, register map, project report
scripts/      Build and setup scripts
```
 
## Team
 
| Name | Role |
|---|---|
| Nhut Phung | Group manager — coordination, keeping the team on schedule, assisting other members |
| Ethan Puga | FPGA development and PCB design, including sensing platform tilt and other signal processing functions |
| Michael (Jaime) Burt | Raspberry Pi, camera integration, and image processing system |
| Fahad Alani | Hardware and mechanical design of the platform; assists with PCB development and Raspberry Pi integration |
| Jalen Lang | FPGA development — control logic, servo interfacing, timing, and other digital system functions |

## Status
 
_In development._