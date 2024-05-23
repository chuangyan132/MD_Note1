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

### What is yield/generator framwork in python?
> The yield statement in Python is used to create a generator function, which is a special type of iterator that can be paused and resumed during iteration. When a generator function is called, it returns a generator object that can be iterated over using a for loop or other iteration constructs. The yield statement is used to yield values from the generator function, allowing it to produce a sequence of values without storing them all in memory at once. This makes generators memory-efficient and suitable for processing large datasets or infinite sequences.

- example
```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

fib = fibonacci(10)
for num in fib:
    print(num)
```

- how to understand yield()
  - used to create a generator function
- What is generator?
  - a special type of iterator that can be paused and resumed during iteration

### 