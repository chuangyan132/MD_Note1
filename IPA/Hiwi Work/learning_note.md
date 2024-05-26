# Learning note
## 5.24
### How to understand async def setup_post_load(self): and setup_scene
```python
def setup_scene(self):
    world = self.get_world()
    world.scene.add_default_ground_plane()
    assets_root_path = get_assets_root_path()
    if assets_root_path is None:
        carb.log_error("Could not find nucleus server with /Isaac folder")
    asset_path = assets_root_path + "/Isaac/Robots/Jetbot/jetbot.usd"
    add_reference_to_stage(usd_path=asset_path, prim_path="/World/Fancy_Robot")
    jetbot_robot = world.scene.add(Robot(prim_path="/World/Fancy_Robot", name="fancy_robot"))
    return

async def setup_post_load(self):
    self._world = self.get_world()
    self._jetbot = self._world.scene.get_object("fancy_robot")
    self._jetbot_articulation_controller = self._jetbot.get_articulation_controller()
    self._world.add_physics_callback("sending_actions", callback_fn=self.send_robot_actions)
    return
```
- Why
  - setup_scene
    - Used to define the initial setup of the simulation scene (synchronously been called)
    - All synchronously functions been executed one by one in order. The programs waits for each task to complete before moving on to the next one
  - setup_post_load
    - Designed for additional setup tasks that should occur after the initial scene has been loaded ()
    - Asynchronous Methods
      - Allows a program to handle multiple tasks at the same time

### How to make jetbot forwards, backwards, and also stop after 5 seconds
```python
# Copyright (c) 2020-2023, NVIDIA CORPORATION. All rights reserved.
#
# NVIDIA CORPORATION and its licensors retain all intellectual property
# and proprietary rights in and to this software, related documentation
# and any modifications thereto. Any use, reproduction, disclosure or
# distribution of this software and related documentation without an express
# license agreement from NVIDIA CORPORATION is strictly prohibited.
#

from omni.isaac.examples.base_sample import BaseSample
from omni.isaac.core.utils.types import ArticulationAction
from omni.isaac.core.utils.nucleus import get_assets_root_path
from omni.isaac.core.utils.stage import add_reference_to_stage
from omni.isaac.core.robots import Robot
import numpy as np
import carb

class HelloWorld(BaseSample):
    def __init__(self) -> None:
        super().__init__()
        self.elapsed_time = 0.0  # Initialize the elapsed time
        self.forward_velocity = 1.0  # Set the desired forward velocity
        return

    def setup_scene(self):
            world = self.get_world()
            world.scene.add_default_ground_plane()
            assets_root_path = get_assets_root_path()
            if assets_root_path is None:
                carb.log_error("Could not find nucleus server with /Isaac folder")
            asset_path = assets_root_path + "/Isaac/Robots/Jetbot/jetbot.usd"
            add_reference_to_stage(usd_path=asset_path, prim_path="/World/Fancy_Robot")
            jetbot_robot = world.scene.add(Robot(prim_path="/World/Fancy_Robot", name="fancy_robot"))
            return

    async def setup_post_load(self):
        self._world = self.get_world()
        self._jetbot = self._world.scene.get_object("fancy_robot")
        # This is an implicit PD controller of the jetbot/ articulation
        # setting PD gains, applying actions, switching control modes..etc.
        # can be done through this controller.
        # Note: should be only called after the first reset happens to the world
        self._jetbot_articulation_controller = self._jetbot.get_articulation_controller()
        # Adding a physics callback to send the actions to apply actions with every
        # physics step executed.
        self._world.add_physics_callback("sending_actions", callback_fn=self.send_robot_actions)
        return

    def send_robot_actions(self, step_size):
        # Every articulation controller has apply_action method
        # which takes in ArticulationAction with joint_positions, joint_efforts and joint_velocities
        # as optional args. It accepts numpy arrays of floats OR lists of floats and None
        # None means that nothing is applied to this dof index in this step
        # ALTERNATIVELY, same method is called from self._jetbot.apply_action(...)

        self.elapsed_time += step_size

        if self.elapsed_time >= 5.0:
            joint_velocities = np.array([0.0, 0.0])

        else:
            joint_velocities = np.array([self.forward_velocity, self.forward_velocity])
        
        
        self._jetbot_articulation_controller.apply_action(ArticulationAction(joint_positions=None,
                                                                            joint_efforts=None,
                                                                            joint_velocities=joint_velocities))
        return
```

### Erros: robot has no attribute: apply_wheel_actions
Start it again. Reason for that is unknow
### How to understand async and await functions 
```python
async def setup_post_load(self):
        self._world = self.get_world()
        self._franka = self._world.scene.get_object("fancy_franka")
        self._fancy_cube = self._world.scene.get_object("fancy_cube")
        # Initialize a pick and place controller
        self._controller = PickPlaceController(
            name="pick_place_controller",
            gripper=self._franka.gripper,
            robot_articulation=self._franka,
        )
        self._world.add_physics_callback("sim_step", callback_fn=self.physics_step)
        # World has pause, stop, play..etc
        # Note: if async version exists, use it in any async function is this workflow
        self._franka.gripper.set_joint_positions(self._franka.gripper.joint_opened_positions)
        await self._world.play_async()
        return
```
- Async def will only been executed after await function is finished
### How to udstand task_params["cube_name"]["value"]
### How to source the modules in any scripts(py)
- Create .vscode
  - add "python.analysis.extraPaths": [] in settings.json
  - e.g.
 "exts/omni.exporter.urdf",
"exts/omni.exporter.urdf/pip_prebundle"
  - Reload the window
### How to understand upstate function
observations.update(self._pick_place_task.get_observations())
It is a specific method available to dictionary-like objects in python
it can be used with any function that returns a dictionary or an iterable of key-value pairs that are compatible with a dictionary.
```python
def get_new_data():
    return {'key2': 'updated_value2', 'key4': 'value4'}

# Existing dictionary
data = {'key1': 'value1', 'key2': 'value2'}

# Update the dictionary with data returned from the function
data.update(get_new_data())

print(data)
# Output: {'key1': 'value1', 'key2': 'updated_value2', 'key4': 'value4'}
```
### How to understand pre_step()
Its been called before stepping the physics simulation
- Guess : Its been called in function self._world.add_physics_callback
- Guess: Its could been managed by some simulation_event_lopp framework, which is not visible in api
### How to understand callbacks()
Its very like the signal-slot in QT
Some logic inside callback function will be executed when some event happend
#### How to use callbacks
```python
import tkinter as tk

# Step 1: Create the main application window
root = tk.Tk()
root.title("Callback Example")
root.geometry("300x200")

# Step 2: Create a callback function
def on_button_click():
    print("Button was clicked!")

# Step 3: Create a button widget and register the callback function
button = tk.Button(root, text="Click Me", command=on_button_click)
button.pack(pady=20)

# Step 4: Start the main event loop
root.mainloop()
```
- Define a callback, register it, having an event_loop to run it.
## 5.25
### Tools to connect with celltower1 file
```python
# Open a terminal, run file
./wifi_clicker.sh
# source code

#!/bin/bash

# Move to a specific position and click
xdotool mousemove 1184 861 click 1

# Wait for 2 seconds
sleep 2

# Move to another position and click
xdotool mousemove 1168 805 click 1

sleep 2
xdotool mousemove 1119 671 click 1
sleep 1

xdotool mousemove 1207 709 click 1
```
### How to understand setup_scene & setup_post_load
- setup_scene
  - Purpose:
    - The setup_scene method is responsible for creating and configuring the initial state of the simulation environment. This includes adding tasks, entities, and objects to the scene.
  - When it is called:
    - It is called during the initial setup phase, before the simulation starts. This method is typically used to define the static aspects of the scene, such as the placement of robots, objects, and other entities.
  - Typical Use Cases:
    - Adding tasks to the simulation world.
    - Defining the initial positions and properties of objects and robots.
    - Setting up the static environment and initial conditions.
- setup_post_load
  - Purpose:
    - The setup_post_load method is responsible for performing additional setup tasks that depend on the simulation environment being fully loaded. This includes initializing controllers, retrieving objects, and registering callbacks that require the full context of the loaded simulation.
  - When it is called:
    - It is called after the simulation environment has been fully loaded. This method is used to set up dynamic aspects of the simulation that depend on the entities and tasks being fully instantiated and available in the scene.
  - Typical Use Cases:
    - Initializing robot controllers.
    - Retrieving objects and entities that were added to the scene.
    - Registering callbacks for simulation events (e.g., physics steps).
    - Performing actions that require the simulation to be in a ready state.
  - 
  
- Key Differences
  1. Timing:
    - setup_scene is called early in the setup process to define the static configuration of the scene.
    - setup_post_load is called after the scene is fully loaded to perform additional setup tasks that require the complete context.
  2. Functionality:
    - setup_scene is used for adding and configuring tasks and static objects.
    - setup_post_load is used for initializing controllers, retrieving objects, and registering callbacks that depend on the fully loaded scene.
  3. Dependencies:
    - setup_scene does not depend on the full scene context and is used to set up the initial state.
    - setup_post_load depends on the scene being fully loaded and is used to perform setup actions that need the full context of the simulation.

How to understand Lambda function 
is_unique_fn=lambda x: not self.scene.object_exists(x)

- What -> anonymous function 
  - Lambda Function: This is an anonymous function defined using the lambda keyword. It takes an argument x and returns the result of not self.scene.object_exists(x).
  - Purpose: This lambda function is used to check if an object with the name x already exists in the scene. It returns True if the object does not exist (not self.scene.object_exists(x)), indicating that the name is unique.
  - 
- Why
  - Allow to write small functions in a compact, readable format
  - Only for short period without a function name
  - Such as map(), filter(), sorted()
- When 
  - Short lived function
  - Inline function
### How to understand def find_unique_string_name(initial_name: str, is_unique_fn: Callable[[str], bool]) -> str: 
- is_unique_fn: Callable[[str], bool]: This specifies that is_unique_fn is expected to be a callable (i.e., a function) that takes a single string argument and returns a boolean value.

### How to understand range

In Python, range is a built-in function used to generate a sequence of numbers. It is commonly used for iteration in loops. 
1. range(stop): Generates numbers from 0 up to, but not including, stop.
2. range(start, stop): Generates numbers from start up to, but not including, stop.
3. range(start, stop, step): Generates numbers from start up to, but not including, stop, incrementing by step.
What is carb module
The carb module is part of the NVIDIA Omniverse ecosystem, specifically within the context of Omniverse Kit and related applications.
Key Features and Services Provided by carb
1. Logging:
The carb module provides a robust logging system that allows developers to output debug information, warnings, errors, and other log messages.
2. Settings Management:
It offers mechanisms to manage application settings, such as configuration files and runtime settings, which can be essential for customizing and controlling application behavior.
3. Event Handling:
The module facilitates event management and dispatching, allowing different parts of an application to communicate and respond to events in a decoupled manner.
4. Plugin Management:
carb supports a plugin system that enables developers to extend and customize functionalities by loading and unloading plugins dynamically.
5. Thread Management:
It provides utilities for managing threads and synchronizing tasks, which is crucial for ensuring the performance and responsiveness of applications.
```python
import carb

# Get a logger instance
logger = carb.logger.get_logger("my_application")

# Output different types of log messages
logger.info("This is an informational message.")
logger.warn("This is a warning message.")
logger.error("This is an error message.")
logger.debug("This is a debug message.")
```
### How to understand tasks[-1]
- List Indexing: In Python, you can access elements of a list using indices. Positive indices start from 0 and go up, accessing elements from the beginning of the list. Negative indices start from -1 and go down, accessing elements from the end of the list.
  - tasks[0] would access the first element.
  - tasks[-1] accesses the last element of the list.
RMPFlowController
URDF file
- OBJ (mesh)
- Link
  - It has two separate meshes associated with it
  - Visual mesh
  - Collision mesh
### MJCF file
### Can not edit usd from isaac asset
- Collect it first locally !