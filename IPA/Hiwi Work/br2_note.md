# Note in br2 project from behavior tree
## br2
### changed in plansys2_hospitial_l4ros2
### how to fix the issue
### halt method
### tick
- how ofer to call tick?
  - 
### What is AMCL?
> AMCL (Adaptive Monte Carlo Localization) is a probabilistic localization algorithm often used in robotics to estimate the pose (position and orientation) of a robot in an environment. It uses a particle filter to represent the posterior distribution of the robot's pose and updates this distribution based on sensor measurements and motion models. AMCL is known for its ability to handle non-linear and multi-modal localization problems, making it suitable for a wide range of robotic applications.

### What is odom transform?
> The odometry transform, often denoted as `odom`, is a transformation that represents the estimated motion of a robot based on wheel encoders or other motion sensors. This transform is typically used in conjunction with other sensor data, such as laser scans or camera images, to estimate the robot's pose in a global reference frame. The odometry transform is essential for robot localization and mapping tasks, as it provides an estimate of the robot's position and orientation over time.

### What is a costmap?
> A costmap is a grid-based representation of the environment used in robot navigation and path planning. It assigns costs to different cells in the grid to represent obstacles, free space, and other relevant information about the environment. Costmaps are commonly used in conjunction with localization and mapping algorithms to help robots plan collision-free paths and avoid obstacles while navigating in complex environments.

