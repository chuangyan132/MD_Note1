# Tutorial to learn CMakeLists.txt
## Explanation of functions
### add_library
```cmake
add_library(<name> [STATIC | SHARED | MODULE]
            [EXCLUDE_FROM_ALL]
            source1 [source2 ...])
```
- is used to define a library target within project
- it represents a collection of compiled souirce files that can be linked with other targets, like executables, to provide functionality
- When we use it
- modularize code
- share code between executables
- create plugins or modules
- build third parties
> each BT node will be compiled as a separate library, we can load them as plugins

### ament_target_dependencies
```cmake
ament_target_dependencies(<target>
                          [dependency1 [dependency2 ...]])
```
- is used to specify dependencies of a target, in ros2
- target is usually a library or an executable

### find_package
```cmake
find_package(<package> [version] [EXACT] [QUIET] [MODULE]
             [REQUIRED] [[COMPONENTS] [components...]]
             [OPTIONAL_COMPONENTS components...]
             [NO_POLICY_SCOPE])
```
- is used to locate a package and load its settings

### target_compile_definitions
```cmake
target_compile_definitions(<target> [BEFORE]
                           <INTERFACE|PUBLIC|PRIVATE> [items1...]
                           [<INTERFACE|PUBLIC|PRIVATE> [items2...] ...])
```
- is used to add preprocessor definitions to a target

### install
- is used to install files
## General Workflow/Example