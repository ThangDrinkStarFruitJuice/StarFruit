# Quick Quick Start using ROS

## Setting up catkin workspace
```bash
# Catkin directory can be any name, i put meowmeow_ws
mkdir meowmeow_ws

# Create a src directory inside for all your packages
cd meowmeow_ws
mkdir src

# Init the src directory with the command
catkin_init_workspace

# Go to top-level and build (next section)
```

## Building packages
- 3 Ways to build your packages

### catkin_make
- Supports cmake flags
- More comfortable if you know [CMake](https://cmake.org/)
- Some commonly used commands
```bash
# Build specific package
# Sometimes doesn't build others after use
catkin_make --only_pkg_with_deps <pkg name>

# Build with latest optimization for C++
catkin_make --DCMAKE_BUILD_TYPE=Release

# Just type this if lazy
catkin_make

# source after building, else ROS won't find the new binaries
source devel/setup.bash
```

### catkin build
- builds everything found in `src`
- Just run `catkin build` at top level
```bash
cd ~/meowmeow_ws
catkin build
source devel/setup.bash
```

### Switch build methods
- To rebuild for any reasons, delete `build` and `devel` directories
```bash
cd ~/meowmeow_ws
rm -rf build devel
```

## Robot Modelling
- Either write your own urdf or copy one from [here](https://robots.ros.org/)
- Another way is to draw your stl and convert to gazebo meshes
    - *Actually most people do this, i was wrong on last meeting*

### Making a robot model 
- Create your package to contain this model
```bash
cd meowmeow_ws/src
catkin_create_pkg meow_bot roscpp
cd meow_bot 
mkdir urdf worlds launch meshes
``` 
- Write your urdf, official tutorial [here](http://wiki.ros.org/urdf/Tutorials)
- I included my noob bot model [here](./src/noob_bot/urdf/noob_bot.xacro)
- Include your sensor plugins options in a gazebo file, sample [here](./src/noob_bot/urdf/noob_bot.gazebo)

### Launching in gazebo
- Launch files are [here](./src/noob_bot/launch)
- 2 important files, one that [launches the robot](./src/noob_bot/launch/noob_bot_description.launch) and [one that launch the
world](./src/noob_bot/launch/empty_world.launch)

## Just want to run this repo for funn
```bash
git clone https://github.com/ThangEatsChickan/meowmeowmeow.git
cd meowmeow_ws
catkin_make / catkin build 
source devel/setup.bash
roslaunch noob_bot empty_world.launch

## On another terminal if you want to move the bot
## Source first, then publish values to the topic that defines robot's velocity
source devel/setup.bash
rostopic pub /cmd_vel <tab to autocomplete, then fill in the values>
##example
rostopic pub /cmd_vel 'linear x:1.0 .... angular:1.0'

```



 



