# QuickNode Devlopment Manual
---

Welcome to the QuickNode Development Manual. This guide will walk you through the process of creating a plugin for QuickNode in Python.

---

## Table of Contents
1. [Keep This in Mind](#keep-this-in-mind)
2. [What is QuickNode](#what-is-quicknode)
3. [How to create a plugin for QN in Python](#how-to-create-a-plugin-for-qn-in-python)
   - [Environment](#environment)
   - [Get to Know PluginBusiness](#get-to-know-pluginbusiness)
   - [Fast Start (With demo: Addition calculator Node)](#fast-start)
   - [Details](#details)
4. [Summary](#summary)

---

## Keep This in Mind
> 1. **Have a clear workflow** in mind before you start.
> 2. Keep code on in **apply function** in one class(/Node)

## What is QuickNode
- QuickNode is a powerful and easy-to-use software, developed by SunDuo's team. It is designed to help users create and manage their own workflow with connected nodes.

## How to create a plugin for QN in Python
### Environment
- python and IDE
- QuickNode installed
- plugincore.dll
- packages (PyQt5, installed by pip)
### Get to Know PluginBusiness
> For your convenience, we have provided a `PluginBusiness` class in the structure of dev project. This class is designed to help you create a plugin in most easy way. So you don't need to pay attention What's goning on about the communication between your exe file and QuickNode. 

Lests go through the structure of prepared project(qn_Test):

- qn_Test
  - createprocess.py
    - **You only need to code here.**
  - main
    - The main entry of the plugin exe. **Nothing to code in this file.**
  - qn_basenode.py
    - included BaseNode class. **Nothing to code in this file.**
  - qn_BasicType.py
    - included BasicType representations and constants. **Nothing to code in this file.**
  - qn_ErroType.py
    - included ErrorType representations and constants. **Nothing to code in this file.**
  - qn_plugincore.py
    - Included Key class and PluginCore class. **Nothing to code in this file.**
  - qn_pluginbusiness.py
    - Included Key communication class and PluginBusiness class. **Nothing to code in this file.**
  - qn_errors.py
    - Included Error class. **Nothing to code in this file.**
  
  




### Fast Start
In this section, we'll walk through a demo of creating an Addition Calculator Node. 
...

### Details
...

## Summary
...
