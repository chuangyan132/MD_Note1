# 7.11
## Main Work
### math lib
- math lib can have mathmatic functions

### userspace
using namespace std::chrono_literals;


how to understand the feedback of 500ms
- which means that the MoveAction class is configured to provide feedback about the action's progress every 500 milliseconds. Here's how to understand and interpret this feedback mechanism:
- MoveAction()
: plansys2::ActionExecutorClient("move", 500ms)

### Common Coordinate Frames in ROS
map: A global, fixed frame of reference, typically used for long-term navigation. This frame is usually static and represents the environment map.
odom: A local frame of reference for odometry, which represents the robot's position relative to its starting point. This frame can drift over time.
base_link: A frame attached to the robot itself, typically at its center. This frame moves with the robot.
camera_link, laser_link, etc.: Frames attached to specific sensors on the robot.


### Determining the Coordinate Frame to Use
The choice of coordinate frame depends on several factors:

Global vs. Local Goals:

Use the map frame for global navigation goals.
Use the odom frame for local navigation and short-term goals.
Sensor Data:

Use sensor-specific frames like camera_link or laser_link for data directly from sensors.
Robot-centric Operations:

Use base_link for operations relative to the robot’s body, such as avoiding obstacles.


### map function
std::map<std::string, geometry_msgs::msg::PoseStamped> waypoints_;
This allows the program to associate descriptive names (like "wp1", "wp2", etc.) with specific poses in space.
- std::map is a standard template library (STL) container in C++ that stores key-value pairs. It provides fast lookup, addition, and removal of elements based on keys. The keys are unique within the map.