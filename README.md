# Robotic Project

This project implements an autonomous robotic system capable of detecting objects, navigating in a dynamic environment, localizing itself, planning paths, and physically grasping a target object.

The system combines **computer vision**, **LIDAR-based mapping & localization**, and **motion control**, running across **Raspberry Pi** and **Arduino** platforms.

## Project Overview

The robot is designed to:

- Detect a green-colored bottle using a camera
- Build and use an environmental map with LIDAR data
- Localize itself using the **Iterative Closest Point (ICP)** algorithm
- Plan an obstacle-free path to the target
- Follow the planned path autonomously
- Grab the detected object using a servo-controlled mechanism

## Key Features

### Object Detection
- Real-time camera-based detection
- Color-based segmentation (green objects)
- Implemented in Python with computer vision libraries

### Localization & Mapping
- 2D LIDAR for environment scanning
- **ICP** algorithm for scan matching and pose estimation
- Map built from recorded LIDAR data

### Path Planning & Navigation
- **A*** algorithm for global path planning
- Smooth path following with local corrections
- Goal-directed autonomous movement

### Object Grasping
- Custom crawler mechanism
- Controlled by high-torque servo motors
- Reliable grasping of cylindrical objects (e.g. bottles)

## Hardware Requirements

- Raspberry Pi (4 recommended) with Python 3
- Arduino board (e.g. Uno / Mega / Nano)
- USB or CSI camera module
- 2D LIDAR sensor (e.g. RPLIDAR, LD06, etc.)
- DC motors + motor driver (e.g. L298N, TB6612, etc.)
- 2–4 high-torque servo motors for crawler/gripper
- Power supply / battery pack suitable for all components

## How to Run

### 1. Raspberry Pi Side (Navigation + Vision + Planning)

Run these scripts **in separate terminals** (in the given order):

#### Terminal 1 – Initialization & sensor interfaces
      cd finalfinal
      python3 init_state.py

#### Terminal 2 – Path planning (once map & target are available)
      python3 path_planning.py

#### Terminal 3 – Path following & control
      python3 path_following.py


### 2. Arduino Side (Low-level Control)

- Navigate to the Arduino code folder: Bashcd main
- Open main.ino in the Arduino IDE
- Select the correct board and port
- Upload the sketch to the Arduino

   Arduino responsibilities:

- Motor PWM / direction control
- Servo actuation for crawler/gripper
- Reading & forwarding sensor data (if any additional sensors)
- Emergency stop / safety logic (if implemented)

## Technologies Used

Python → high-level logic, vision, ICP, planning, ROS2 nodes
Arduino (C/C++) → real-time motor & servo control
Computer Vision → color-based object detection
LIDAR → mapping & obstacle detection
Iterative Closest Point (ICP) → scan matching & localization
A* → global path planning
ROS2 → LIDAR data recording, replay, inter-process communication (optional)
