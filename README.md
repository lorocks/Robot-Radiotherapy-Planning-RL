# RL Training for a Unified Framework for Robotic Radiotherapy Planning

This is a repo that trains an Reinforcement Learning agent using a robot in RViz where the enviornment is a rendering of a point cloud.
The observation is the 2D view of the point cloud taken from a camera attached on the robot end-effector.

```bash
  ros2 launch lab_simulation_gazebo lab_sim_moveit.launch.py ur_type:=ur3e description_package:=lab_description description_file:=lab.urdf.xacro moveit_config_package:=lab_moveit_config moveit_config_file:=lab.srdf.xacro runtime_config_package:=lab_simulation_gazebo launch_rviz:=false
```