SIT-AIR

Autonomous Intelligence & Robotics Platform

SIT-AIR is an open-source autonomous aerial robotics project being designed and built by students to explore the intersection of drone engineering, robotics, edge AI, computer vision, and autonomous systems.

The project aims to develop a complete drone platform from the ground up using open-source software, commercially available components, locally running AI models, and reproducible engineering practices.

Build the aircraft. Build the autonomy. Build the intelligence.

⸻

🚧 Project Status

Status: Early Development / Architecture & Simulation

The project is currently establishing its hardware architecture, simulation environment, robotics stack, and software foundation.

Current focus

* [ ]	System architecture
* [ ]	Hardware selection
* [ ]	PX4 simulation
* [ ]	ROS 2 integration
* [ ]	Gazebo simulation
* [ ]	Basic autonomous mission
* [ ]	Physical flight controller integration
* [ ]	Companion computer integration
* [ ]	Computer vision
* [ ]	Edge AI
* [ ]	Natural-language mission interface
* [ ]	Autonomous navigation

⸻

🎯 Vision

SIT-AIR aims to evolve from a basic quadcopter into a modular autonomous robotics platform capable of:

* Autonomous flight
* GPS-based navigation
* Mission planning
* Computer vision
* Object detection
* Obstacle awareness
* Natural-language interaction
* Local AI inference
* Visual scene understanding
* Autonomous inspection
* Campus-scale robotics experiments

The long-term goal is not simply to build a drone, but to create an open robotics platform on which students can experiment with real-world AI and autonomous systems.

⸻

🧠 Core Idea

The project separates safety-critical flight control from high-level intelligence.

                    HUMAN
                      │
              Voice / Dashboard
                      │
                      ▼
              ┌───────────────┐
              │   AI Layer    │
              │               │
              │ LLM / VLM     │
              │ Vision        │
              │ Speech        │
              └───────┬───────┘
                      │
                Mission Intent
                      │
                      ▼
              ┌───────────────┐
              │   Autonomy    │
              │               │
              │ Mission       │
              │ Planning      │
              │ Navigation    │
              └───────┬───────┘
                      │
                    ROS 2
                      │
               PX4 ROS 2 API
                      │
                      ▼
              ┌───────────────┐
              │     PX4       │
              │ Flight Stack  │
              └───────┬───────┘
                      │
               Flight Control
                      │
             ┌────────┴────────┐
             ▼                 ▼
          Sensors           Motors

Design principle

The AI system should never directly control individual motors.

Instead:

Natural Language
       ↓
AI
       ↓
Structured Mission
       ↓
Validation
       ↓
Autonomy / Planner
       ↓
PX4
       ↓
Flight Controller
       ↓
Motors

This separation allows experimentation with AI while keeping low-level flight control deterministic and independent.

⸻

🏗️ System Architecture

SIT-AIR consists of several major layers.

┌─────────────────────────────────────────────────────┐
│                    USER INTERFACE                   │
│              Web Dashboard / Voice                 │
└──────────────────────────┬──────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────┐
│                    AI PLATFORM                      │
│       LLM │ VLM │ Computer Vision │ Speech         │
└──────────────────────────┬──────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────┐
│                 AUTONOMY ENGINE                     │
│ Mission Planning │ Navigation │ Behavior            │
└──────────────────────────┬──────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────┐
│                       ROS 2                         │
│ Nodes │ Topics │ Services │ Actions │ TF2           │
└──────────────────────────┬──────────────────────────┘
                           │
                    PX4 ROS 2 Interface
                           │
┌──────────────────────────▼──────────────────────────┐
│                       PX4                           │
│ State Estimation │ Control │ Failsafes │ Flight    │
└──────────────────────────┬──────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────┐
│                    HARDWARE                         │
│ Pixhawk │ ESC │ Motors │ GPS │ IMU │ Battery       │
└─────────────────────────────────────────────────────┘

PX4 provides deep ROS 2 integration, including access to PX4 uORB topics and the ability to implement custom flight behavior through ROS 2. PX4 currently recommends ROS 2 Jazzy on Ubuntu 24.04 for this workflow. (PX4 Documentation)

⸻

🛠️ Technology Stack

Flight Control

Technology	Role
PX4 Autopilot	Flight-control firmware
Pixhawk-class flight controller	Real-time flight computer
MAVLink	Vehicle communication
C/C++	Flight/control software

PX4 remains responsible for:

* Attitude stabilization
* Rate control
* Position control
* Sensor integration
* Flight modes
* Failsafes
* Motor control
* Battery monitoring
* Return-to-home behavior

⸻

🤖 Robotics

Technology	Role
ROS 2 Jazzy	Robotics middleware
Ubuntu 24.04	Primary development OS
DDS / uXRCE-DDS	PX4 ↔ ROS 2 communication
TF2	Coordinate transformations
RViz 2	Visualization
rosbag	Data recording
Colcon	ROS workspace/build system

ROS 2 Jazzy is the primary target for the project. Ubuntu 22.04 + ROS 2 Humble can remain a compatibility option where required by existing hardware or software. (PX4 Documentation)

⸻

🧪 Simulation

Technology	Role
Gazebo Harmonic	Physics simulation
PX4 SITL	Simulated flight controller
ROS 2	Robotics integration
RViz 2	Visualization
ros_gz	ROS 2 ↔ Gazebo integration

The initial development target is:

Ubuntu 24.04
       │
ROS 2 Jazzy
       │
Gazebo Harmonic
       │
PX4 SITL
       │
SIT-AIR ROS 2 packages

Gazebo currently identifies Ubuntu 24.04 + ROS 2 Jazzy + Gazebo Harmonic as its recommended new-user setup. (Gazebo Sim)

⸻

🖥️ Companion Computer

Primary target

Raspberry Pi 5

The companion computer is responsible for:

* ROS 2
* Computer vision
* Camera processing
* Mission logic
* AI inference
* Telemetry
* Voice processing
* High-level autonomy

Edge AI accelerator

Raspberry Pi AI HAT+ 2

Target capabilities include:

* Computer vision
* Object detection
* Local LLM inference
* Local VLM inference
* Edge AI experimentation

The AI HAT+ 2 uses a Hailo-10H accelerator rated at up to 40 TOPS INT4 and includes 8 GB of onboard memory for generative-AI workloads. (Raspberry Pi)

⸻

👁️ Computer Vision

The perception stack will be modular.

Camera
   │
   ▼
Image Pipeline
   │
   ├── Object Detection
   ├── Tracking
   ├── Segmentation
   ├── Depth
   └── Scene Understanding

Planned technologies

* OpenCV
* YOLO-family models
* ONNX / hardware-accelerated inference where appropriate
* Hailo inference stack
* Camera calibration tools
* Open-source tracking algorithms

The exact model will remain replaceable so the platform does not become dependent on one AI model.

⸻

🧠 Local AI

SIT-AIR is designed around edge-first AI.

AI components

                    AI PLATFORM
                        │
       ┌────────────────┼────────────────┐
       │                │                │
      LLM              VLM             Vision
       │                │                │
   Planning        Scene reasoning   Detection
       │                │                │
       └────────────────┼────────────────┘
                        │
                  Mission Engine

LLM

The LLM is responsible for:

* Natural-language understanding
* Mission interpretation
* High-level planning
* Tool selection
* Structured command generation

Example:

"Inspect the entrance of the engineering building."

becomes:

{
  "mission": "inspect",
  "target": "engineering_building_entrance",
  "requirements": {
    "capture_images": true,
    "return_to_home": true
  }
}

The mission engine validates the generated command before execution.

⸻

👀 Vision-Language Model

A VLM can provide higher-level scene understanding.

Example:

Camera
   ↓
Vision / VLM
   ↓
Scene Description
   ↓
Mission System

Potential applications:

* Scene description
* Landmark recognition
* Visual question answering
* Object-context understanding
* Inspection assistance

⸻

🎙️ Voice Interface

Planned architecture:

Microphone
    ↓
Speech-to-Text
    ↓
LLM
    ↓
Mission Command
    ↓
Validation
    ↓
ROS 2

Target interaction:

“Take off to five meters and inspect the marked area.”

The drone should translate this into a structured mission rather than sending raw natural-language commands directly to PX4.

⸻

🧭 Autonomous Navigation

Future navigation capabilities include:

* GPS waypoint navigation
* Position hold
* Mission execution
* Obstacle awareness
* Path planning
* Visual navigation
* SLAM
* Visual odometry
* Geofencing
* Autonomous return

The navigation stack will remain independent of the LLM.

LLM
 │
 ▼
Mission
 │
 ▼
Mission Planner
 │
 ▼
Navigation
 │
 ▼
PX4

⸻

🌐 Ground Station

A web-based ground station is planned for monitoring and experimentation.

Frontend

* Next.js
* React
* TypeScript
* Tailwind CSS
* Map visualization
* Telemetry dashboard

Backend

* Python
* FastAPI
* WebSocket
* ROS 2 integration

Dashboard capabilities

* Live telemetry
* Battery
* GPS
* Position
* Altitude
* Flight mode
* Mission status
* Camera stream
* AI status
* System health
* Mission logs

⸻

🗄️ Data & Logging

The system will record:

* Flight telemetry
* ROS 2 topics
* Mission events
* AI decisions
* Camera metadata
* System diagnostics
* Errors
* Safety events

Planned technologies

* rosbag2
* SQLite
* PostgreSQL
* Structured JSON logs

A major project objective is making autonomous decisions observable and reproducible.

⸻

📁 Repository Structure

sit-air/
│
├── README.md
│
├── docs/
│   ├── architecture/
│   ├── design/
│   ├── hardware/
│   ├── simulation/
│   ├── safety/
│   ├── research/
│   └── development/
│
├── firmware/
│   └── px4/
│
├── ros2/
│   ├── sit_air_bringup/
│   ├── sit_air_interfaces/
│   ├── sit_air_mission/
│   ├── sit_air_navigation/
│   ├── sit_air_perception/
│   ├── sit_air_control/
│   └── sit_air_telemetry/
│
├── ai/
│   ├── llm/
│   ├── vlm/
│   ├── vision/
│   ├── speech/
│   └── agent/
│
├── simulation/
│   ├── gazebo/
│   ├── worlds/
│   ├── models/
│   └── px4/
│
├── ground-station/
│   ├── frontend/
│   └── backend/
│
├── hardware/
│   ├── cad/
│   ├── electronics/
│   ├── wiring/
│   ├── pcb/
│   └── bom/
│
├── scripts/
│
├── tests/
│
├── docker/
│
└── .github/
    ├── workflows/
    ├── ISSUE_TEMPLATE/
    └── pull_request_template.md

⸻

🔧 Hardware Architecture

Flight System

* Quadrotor frame
* Brushless motors
* ESCs
* Propellers
* Flight controller
* Power module
* LiPo battery
* GPS
* Compass
* RC receiver
* Telemetry radio

Companion System

* Raspberry Pi 5
* AI HAT+ 2
* Camera
* Optional depth camera
* Microphone
* Speaker
* Storage

Future Sensors

* LiDAR
* Optical flow
* Depth camera
* Additional IMUs
* Range sensors

⸻

🧩 Development Phases

Phase 1 — Simulation

* [ ]	PX4 SITL
* [ ]	Gazebo Harmonic
* [ ]	ROS 2 Jazzy
* [ ]	Basic vehicle model
* [ ]	Telemetry
* [ ]	Takeoff
* [ ]	Landing
* [ ]	Waypoint mission

Phase 2 — Flight Controller

* [ ]	Select flight controller
* [ ]	PX4 installation
* [ ]	Sensor calibration
* [ ]	ESC configuration
* [ ]	Motor testing
* [ ]	Manual flight

Phase 3 — Autonomous Flight

* [ ]	GPS
* [ ]	Position hold
* [ ]	Return-to-home
* [ ]	Autonomous waypoint missions
* [ ]	Safety testing

Phase 4 — Companion Computer

* [ ]	Raspberry Pi 5
* [ ]	ROS 2
* [ ]	Camera
* [ ]	Telemetry connection
* [ ]	AI accelerator

Phase 5 — Perception

* [ ]	Camera pipeline
* [ ]	Object detection
* [ ]	Tracking
* [ ]	Depth
* [ ]	Visual telemetry

Phase 6 — AI

* [ ]	Local LLM
* [ ]	Local VLM
* [ ]	Speech-to-text
* [ ]	Mission parser
* [ ]	Tool-calling interface
* [ ]	Structured mission schema

Phase 7 — Autonomy

* [ ]	Mission planner
* [ ]	Navigation
* [ ]	Obstacle awareness
* [ ]	Path planning
* [ ]	Autonomous inspection

Phase 8 — Campus Robotics

* [ ]	Campus map
* [ ]	Landmark recognition
* [ ]	Inspection missions
* [ ]	AI-assisted reporting
* [ ]	Multi-mission operation

⸻

🧪 Testing Strategy

SIT-AIR follows a simulation-first development model.

Unit Test
    ↓
Software-in-the-Loop
    ↓
Simulation
    ↓
Hardware-in-the-Loop
    ↓
Bench Test
    ↓
Controlled Flight
    ↓
Autonomous Flight

No new autonomous behavior should be tested directly on an uncontrolled physical aircraft.

⸻

🔐 Safety Principles

Safety-critical systems take priority over AI capabilities.

Core principles

1. AI cannot directly control motors.
2. PX4 remains responsible for low-level flight control.
3. Autonomous missions require validation.
4. Flight boundaries must be enforced.
5. Manual override must always be available.
6. Loss-of-link behavior must be defined.
7. Battery failsafes must be configured.
8. Autonomous features must be tested in simulation first.
9. Outdoor testing must follow applicable aviation and campus rules.
10. AI failures must fail safely rather than continue executing an invalid mission.

⸻

🧑‍💻 Development Philosophy

SIT-AIR follows these principles:

Open Source First

Prefer open-source:

* Firmware
* Robotics middleware
* AI models
* Development tools
* Simulation
* Libraries

Modular

Every major subsystem should be replaceable.

LLM
 ↑
Can be replaced
Vision
 ↑
Can be replaced
Camera
 ↑
Can be replaced
Companion Computer
 ↑
Can be replaced
Flight Controller
 ↑
Can be replaced

Simulation First

New autonomy capabilities should first work in simulation.

Reproducible

Another student should be able to clone the repository and reproduce the development environment.

Research Friendly

The platform should make it easy to add experimental algorithms without rewriting the complete system.

⸻

🎓 Educational Objectives

SIT-AIR is designed as a multidisciplinary student project.

Electronics

* Motors
* ESCs
* Batteries
* Power systems
* Sensors
* Embedded systems

Robotics

* ROS 2
* Coordinate frames
* Localization
* Navigation
* SLAM
* Motion planning

AI

* Computer vision
* Edge inference
* LLMs
* VLMs
* Agents
* Multimodal AI

Software Engineering

* Python
* C++
* TypeScript
* APIs
* Distributed systems
* Testing
* CI/CD
* Docker

Research

The platform can support experiments in:

* Autonomous navigation
* Edge AI
* Vision-language robotics
* Natural-language robotics
* AI planning
* Human-robot interaction
* Multi-modal perception
* Autonomous inspection

⸻

🤝 Contribution

SIT-AIR is intended to be a collaborative student engineering project.

Contributions are welcome across:

* Hardware
* Firmware
* ROS 2
* Computer vision
* AI
* Simulation
* Web development
* Mechanical design
* Documentation
* Testing
* Research

Suggested workflow

Issue
  ↓
Design / Discussion
  ↓
Implementation
  ↓
Simulation Test
  ↓
Hardware Test
  ↓
Pull Request
  ↓
Review
  ↓
Merge

⸻

🗺️ Roadmap

V0 — Digital Drone

PX4 + ROS 2 + Gazebo

V1 — Physical Drone

Manual flight + PX4

V2 — Autonomous Drone

GPS missions + telemetry

V3 — Seeing Drone

Camera + computer vision

V4 — Edge AI Drone

Raspberry Pi + AI accelerator

V5 — Conversational Drone

Voice + LLM

V6 — Autonomous AI Drone

LLM/VLM + perception + navigation

V7 — SIT Autonomous Robotics Platform

Reusable platform for multiple student robotics projects.

⸻

📊 Target Architecture

                    ┌─────────────────────┐
                    │      SIT-AIR        │
                    │   AI Drone Platform │
                    └──────────┬──────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
          ▼                    ▼                    ▼
      HARDWARE              ROBOTICS                AI
          │                    │                    │
     Pixhawk                 ROS 2                 LLM
     Motors                  PX4                  VLM
     ESC                     Gazebo               Vision
     GPS                     Navigation           Speech
     IMU                     Planning             Agents
     Camera                  TF2                  Edge AI
          │                    │                    │
          └────────────────────┼────────────────────┘
                               │
                               ▼
                       AUTONOMOUS SYSTEM
                               │
                               ▼
                         REAL WORLD DRONE

⸻

📜 License

This project will use an open-source license appropriate for the project’s hardware designs, software, documentation, and third-party dependencies.

Individual components remain subject to their respective upstream licenses.

⸻

⚠️ Disclaimer

SIT-AIR is an educational and research project.

Autonomous aircraft must be operated responsibly and in accordance with applicable aviation regulations, local airspace restrictions, institutional policies, and safety procedures.

Never test autonomous flight in an uncontrolled environment.

⸻

👥 Project

SIT-AIR — Autonomous Intelligence & Robotics

Built by students interested in:

AI × Robotics × Drones × Open Source × Autonomous Systems

From code to cognition. From simulation to flight.