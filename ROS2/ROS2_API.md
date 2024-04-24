# API
## launch
- support to use in python, XML, YAML

## colcon
- how to sorce the structure in one folder
```
sudo apt-get update
sudo apt-get install tree

tree -L 1
```
- source the environment
```
source install/setup.bash
```
> When colcon has completed building successfully, the output will be in the install directory. Before you can use any of the installed executables or libraries, you will need to add them to your path and library paths. colcon will have generated bash/bat files in the install directory to help set up the environment. These files will add all of the required elements to your path and library paths as well as provide any bash or shell commands exported by packages.

- how to write a build file
> colcon uses the package.xml specification defined in REP 149 (format 2 is also supported).
- colcon build types
    - ament_cmake
    - ament_python
    - cmake
- build ament_python 
setup.py is main entry point.

- why resolve dependencies
> Before building the workspace, you need to resolve the package dependencies. You may have all the dependencies already, but best practice is to check for dependencies every time you clone. You wouldn’t want a build to fail after a long wait only to realize that you have missing dependencies.
```bash
# cd if you're still in the ``src`` directory with the ``ros_tutorials`` clone
cd ..
rosdep install -i --from-path src --rosdistro humble -y
```

- how to build only one package
```bash
colcon build --packages-select <package_name>
```

- source the enviroment after build package
```bash
source install/setup.bash
```





