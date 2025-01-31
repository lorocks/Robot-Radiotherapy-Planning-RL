# RL Training for a Unified Framework for Robotic Radiotherapy Planning

This is a repo that trains an Reinforcement Learning agent using a robot in RViz where the enviornment is a rendering of a point cloud.
The observation is the 2D view of the point cloud taken from a camera attached on the robot end-effector.

```bash
  ros2 launch lab_simulation_gazebo lab_sim_moveit.launch.py ur_type:=ur3e description_package:=lab_description description_file:=lab.urdf.xacro moveit_config_package:=lab_moveit_config moveit_config_file:=lab.srdf.xacro runtime_config_package:=lab_simulation_gazebo launch_rviz:=false

  ros2 launch launch_robot lab_sim_moveit.launch.py ur_type:=ur3e description_package:=launch_robot description_file:=lab.urdf.xacro moveit_config_package:=robot_moveit_config moveit_config_file:=lab.srdf.xacro runtime_config_package:=<ur_controller ros2_controllers> launch_rviz:=false
```


## Rewards
The reward for actions performed is given based on the distance of the centroid of the green object from the center of the image. There is a special condition where if the green object disappears from the image, a negative reward is given.

Reward tiers are as follows,
 - when green disappears, -1
 - when D(g) = 0, (1/E) + 1
 - when green is present in image, 1/(D(g) + E)

$R(s) = \begin{cases}  
  \frac{1}{D(g) + \epsilon}, & \text{when green is present in the image}\\
  \frac{1}{\epsilon} + 1, & \text{when $D(g) = 0$ }\\
  -1, & \text{when green disappears from the image}
\end{cases}$

Here, D(g) is the distance between the centroid of the green object and the center of the camera image and E is a small number where 0 < E < 1.

Curently the rewards do not take into account the depth from the required target.

## Question to be answered
How many features and depth of convolution is required for the network to learn depth and color at the same time

