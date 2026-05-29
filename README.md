# joint_state_transformer_example

This repository demonstrates the usage of the **joint_state_transformer** for constrained robot kinematics. It enables the transformation of joint states for robots with closed kinematic chains and passive joints.  Each robot is provided as its own package. The robot-specific URDF and meshes are provided in the **descriptions** package.

The *joint_state_transformer* provides forward and inverse kinematics for closed-loop systems:

- Inverse kinematics: end-effector trajectory -> **joint_state_transformer** -> active joint trajectory
- Forward kinematics: measured joint states (subset of all joints) -> **joint_state_transformer** -> full joint state (including passive joints)

The following robots are supported at the moment:

- Autonox *A_00036* 4-DoF Delta robot with a telescopic shaft

Additional robots will be added in the future.

The repository includes the following packages:

- **urdfdom_headers** fork: adds the constraints to the URDF
- **urdfdom** fork: parses the extended URDF with the constraints
- **pinocchio**: used for kinematic tree calculations. Requires recompilation due to the custom **urdfdom** fork
- **robot_model**: solves constraint equations for closed-loop structures
- **joint_state_transformer** package: uses the **robot_model** to transform the trajectory and calculate the passive angles
- **descriptions**: provides the URDF files and meshes for the robots
- robot-specific MoveIt packages: provide a simple demonstration with RViz using the demo.launch.py

## Prerequisites

- Docker
- A running X server as a display

## Usage

1. Initialize the submodules

   ```bash
   git submodule update --init --recursive
   ```

2. Start the container

   ```bash
   docker compose up
   ```  

3. Inside the container: Build (this may take a while)

   ```bash
   colcon build
   source install/setup.bash
   ```

4. Inside the container: Start joint_state_transformer

   ```bash
   ros2 launch joint_state_transformer joint_state_transformer.launch.py
   ```

5. Inside the container: Start the demo

   ```bash
   ros2 launch <chosen_robot_model> demo.launch.py
   ```

## Roadmap

- Add more examples (e.g. the Para-Engineer robots)
  
## Acknowledgement

The repository is developed and maintained by Heilbronn University of Applied Sciences

Supported by Autonox robotics GmbH
