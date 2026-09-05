# SDV Dashboard

### A Lightweight Web-Based Dashboard for ROS 2 Robot Monitoring, Visualization, and Control

SDV Dashboard is a lightweight, browser-based interface designed for monitoring, visualizing, and controlling a ROS 2 robot. It provides a simple and responsive interface for viewing real-time robot data, controlling robot motion, setting navigation goals, and monitoring camera and telemetry information.

The dashboard is implemented as a single HTML file using HTML, CSS, and JavaScript. It connects directly to ROS 2 through `rosbridge_suite` using `roslibjs`, without requiring a separate web backend or build system.

---

## Features

- Real-time ROS 2 robot monitoring
- Live 2D occupancy grid map visualization
- LiDAR scan visualization
- Robot pose tracking
- Global and local path visualization
- Nav2 goal setting using the map
- Keyboard-based teleoperation using WASD
- On-screen joystick control
- Adjustable linear and angular velocity
- Emergency Stop (E-STOP)
- Live camera streaming through MJPEG
- Real-time telemetry display
- Configurable robot IP address
- Configurable ROS 2 topics
- Responsive web-based interface
- Single-file frontend with no build system required

---
## How It Works

The dashboard runs directly in a web browser and communicates with the ROS 2 robot through WebSocket and HTTP connections.

```text
                    ┌─────────────────────────┐
                    │       Web Browser       │
                    │                         │
                    │      SDV Dashboard      │
                    │      HTML/CSS/JS        │
                    └────────────┬────────────┘
                                 │
                  WebSocket / HTTP Connections
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
        ┌────────▼─────────┐           ┌────────▼─────────┐
        │  rosbridge_suite │           │  Camera Server   │
        │    WebSocket     │           │   MJPEG Stream   │
        │     :9090        │           │      :8080       │
        └────────┬─────────┘           └──────────────────┘
                 │
                 │ ROS 2 Topics
                 │
        ┌────────▼─────────┐
        │     ROS 2        │
        │      Robot       │
        └──────────────────┘
```
---
## ROS 2 Topics

The dashboard works with the following ROS 2 topics and interfaces:

| Purpose | Interface |
|---|---|
| Robot velocity | `/cmd_vel` |
| Robot odometry | `/odom` |
| Transform data | `/tf` |
| LiDAR | `/scan` |
| Map | `/map` |
| Global costmap | `/global_costmap/costmap` |
| Navigation path | `/plan` |
| Local path | `/local_plan` |
| Navigation goal | `/goal_pose` |

The map and camera topics can be configured from the dashboard interface.

---
## Robot Control

The dashboard provides multiple methods for controlling the robot.

### Keyboard Control

The robot can be controlled using the following keys:

- **W** – Move Forward
- **S** – Move Backward
- **A** – Turn Left
- **D** – Turn Right

The dashboard also provides adjustable controls for:

- Linear velocity
- Angular velocity

### Joystick Control

An on-screen joystick is provided for interactive robot movement. The current linear and angular velocity values are displayed in the interface.

### Emergency Stop

The **E-STOP** button provides an immediate stop command through the robot velocity interface.

For safe operation, the dashboard should only be used in a controlled environment and with appropriate robot-side safety mechanisms.

---
## Navigation

The dashboard supports basic navigation interaction with ROS 2 Nav2.

Users can:

- View the robot's current position
- Track the robot on the map
- Select a navigation goal directly on the map
- Send the goal to the robot
- Cancel the current navigation goal
- Return the map view to the robot
- Zoom and center the map

The navigation goal is published through the `/goal_pose` topic.

---
## Camera Streaming

The dashboard supports live camera visualization using an MJPEG stream.

The camera stream is provided separately from the ROS 2 WebSocket connection and can be accessed through the robot's camera server.

Typical camera stream configuration:

```text
http://<robot-ip>:8080/stream
```

---
## Telemetry

The dashboard displays useful real-time robot information, including:

- Robot position
- Robot orientation
- Linear velocity
- Angular velocity
- Connection status
- Navigation status

This allows the operator to monitor the robot while controlling or navigating it.

---
## Requirements

Before running the dashboard, the robot-side system should provide:

- ROS 2
- `rosbridge_suite`
- A running ROS 2 robot system
- A compatible camera streaming service for MJPEG video
- A modern web browser
- Network connectivity between the browser and robot

The dashboard itself does not require:

- `package.json`
- Node.js
- npm
- Webpack
- Vite
- A separate web server
- A custom backend

The dashboard is designed to run as a lightweight static web application.

---
## How to Run

### 1. Start the ROS 2 System

Start the required ROS 2 nodes and robot services on the robot.

Make sure the required topics such as `/odom`, `/scan`, `/map`, and `/cmd_vel` are available.

### 2. Start rosbridge

Start `rosbridge_suite` on the robot.

The dashboard expects the WebSocket connection through port `9090`.

The connection follows this format:

```text
ws://<robot-ip>:9090
```

---

## Project Structure

```text
SDV-Dashboard/
├── paper/
│   └── SDV-Dashboard-Research-Paper.pdf
├── README.md
└── index.html
```

---
## Safety and Security

The dashboard is intended for use on a trusted local network.

The default WebSocket and HTTP connections use:

- `ws://`
- `http://`

These connections are not encrypted and do not provide authentication by default.

Therefore:

- Do not expose the dashboard or robot services directly to the public internet.
- Use the dashboard only on a trusted network.
- Configure appropriate network security measures when required.
- Ensure robot-side safety mechanisms are active.
- Test the Emergency Stop function before operating the robot.
- Use appropriate command timeout or watchdog mechanisms on the robot.

The dashboard should be considered an operator interface and not a replacement for hardware-level or robot-side safety systems.

---
## Evaluation

The dashboard was evaluated during practical operation with a ROS 2 robot system.

The evaluation focused on:

- Connection establishment
- Robot control responsiveness
- Emergency Stop response
- Camera streaming
- Map visualization
- LiDAR visualization
- Telemetry updates
- Browser resource usage

The results demonstrated that a lightweight browser-based interface can provide real-time monitoring and basic robot control without requiring a dedicated web backend.

---
## Research Paper

The detailed design, implementation, and evaluation of the SDV Dashboard are presented in the associated IEEE research paper.

📄 **[Read the Research Paper](paper/SDV-Dashboard-Research-Paper.pdf)**

---
## Project Contribution

The project demonstrates how a single-file web application can be used as a lightweight interface for ROS 2 robot monitoring and control.

The main contribution is the integration of:

- ROS 2 communication through `rosbridge_suite`
- Browser-based robot visualization
- LiDAR and map rendering
- Robot teleoperation
- Navigation goal interaction
- Camera streaming
- Real-time telemetry
- Emergency Stop functionality

The approach reduces frontend deployment complexity while providing a practical interface for robot operation and monitoring.

---
## Acknowledgement

This work was developed as part of research and development activities at:

**GITAM Deemed to be University, Bengaluru, India**

---
## License

This project is intended for research and educational purposes.

If you plan to distribute or reuse the code, please add an appropriate open-source license to the repository.

---

### SDV Dashboard

**ROS 2 | Web-Based Robotics | Robot Monitoring | Teleoperation | Navigation**
