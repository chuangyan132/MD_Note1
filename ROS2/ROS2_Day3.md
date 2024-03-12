# Day3

## Topic
### 动作：完整行为的流程管理
![](images/2024-03-12-21-44-23.png)   
> 动作是应用层的通信机制
> 其地层就是基于话题和服务来实现 
#### 实现一个机器人画圆的动作
![](images/2024-03-12-21-51-37.png)
  - enable
  - finish
  - state
### The difference between from and import in python
- 共同点
  - 都用于倒入模块到当前的命名空间,以便可以直接使用模块中的函数和变量
- 不同点
  - import 用于导入整个模块,需要通过模块名来访问模块中的函数和变量
  - from...import 用于导入模块中的指定函数和变量,可以直接使用这些函数和变量,而不需要通过模块名来访问
  - such as import math, math.sqrt(4) and from math import sqrt, sqrt(4)
- 使用 import 由于需要通过模块名来访问属性，因此可以避免属性名冲突
- 当导入模块较小，或者确实需要模块中大部分的功能时，使用 import
- 当只需要模块中部分功能，或者模块中的属性名可能会和当前命名空间中的属性名冲突时，使用 from...import

### 机器人系统的全局字典
> 参数类似于C语言的全局变量.可以在多个节点当中访问和使用
- 参数
  - 全局共享字典
  - 由键值组成
  - 可实现动态监控

- 查看ros2 参数
  ```shell
  ros2 param
  ros2 param list
  ros2 param describe turtlesim background_b // 查看参数的描述
  ros2 param get turtlesim background_b // 获取参数的值
  ros2 param set turtlesim background_b 255 // 设置参数的值
  ```
- You should set the parameters in a init file.
```shell
// print the parameters
ros2 param dump turtlesim
// set the parameters to the ini file(重定向保存)
ros2 param dump turtlesim >> turtlesim.yaml
// why yaml file -> easy understanding

```

- load the parameters from the ini file
```shell
ros2 param load turtlesim turtlesim.yaml
```

### 分布式通信:多计算平台的任务分配
> 将自动化任务分配到多台计算平台上能够减轻单台计算平台的负担，提高整体的运行效率

- 树莓派
  - 电机驱动,传感器采集
- PC
  - 可以进行复杂的算法计算,图像处理,图像识别等

#### 树莓派配置
![](images/2024-03-12-23-18-26.png)

- ip adress on linux
- ipconfig on windows
- ssh pi@
- ifconfig on linux
  
#### 分布式DOMAIN配置