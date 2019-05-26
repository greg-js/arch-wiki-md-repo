[ROS](http://www.ros.org) is an open-source, meta-operating system for your robot. It provides the services you would expect from an operating system, including hardware abstraction, low-level device control, implementation of commonly-used functionality, message-passing between processes, and package management.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation Instructions](#Installation_Instructions)
*   [2 Older Versions (Not fully working)](#Older_Versions_(Not_fully_working))
    *   [2.1 Kinetic](#Kinetic)
*   [3 catkin_make](#catkin_make)
    *   [3.1 Using Catkin/ROS with an IDE](#Using_Catkin/ROS_with_an_IDE)
        *   [3.1.1 CLion](#CLion)
*   [4 catkin build](#catkin_build)
*   [5 Rebuild when shared libraries are updated](#Rebuild_when_shared_libraries_are_updated)
*   [6 Ros 2](#Ros_2)
    *   [6.1 Building from source](#Building_from_source)
    *   [6.2 Usage Examples](#Usage_Examples)

## Installation Instructions

You can install any of the ROS distributions below since they are fully released on AUR.

Melodic [ros-melodic-desktop-full](https://aur.archlinux.org/packages/ros-melodic-desktop-full/)

Lunar [ros-lunar-desktop-full](https://aur.archlinux.org/packages/ros-lunar-desktop-full/)

## Older Versions (Not fully working)

### Kinetic

Kinetic packages on the AUR are a work in progress. There are [some issues regarding opencv3](https://github.com/bchretien/arch-ros-stacks/issues/57#issuecomment-228612399) that have not been fully resolved yet (installing [ros-kinetic-opencv3](https://aur.archlinux.org/packages/ros-kinetic-opencv3/) works, but is somewhat inefficient since it rebuilds opencv3). Currently, installing a metapackage such as [ros-kinetic-ros-core](https://aur.archlinux.org/packages/ros-kinetic-ros-core/) or [ros-kinetic-robot](https://aur.archlinux.org/packages/ros-kinetic-robot/) should bring in all required dependencies (see [[1]](https://paste.xinu.at/YXIz/) for the correct order).

Packages are being added on an as-needed basis. Please post any issues with the current packages in their respective AUR comments section.

## catkin_make

Note that catkin uses python2, and therefore catkin_make may fail unless it explicitly uses python2\. To do so, add the following alias to ~/.bashrc:

```
alias catkin_make="catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so"

```

Another way is to use [python-catkin_tools](https://aur.archlinux.org/packages/python-catkin_tools/) and to configure it by running the following command in your Catkin workspace.

```
catkin config --cmake-args -DPYTHON_EXECUTABLE=/usr/bin/python

```

### Using Catkin/ROS with an IDE

#### CLion

To make [CLion](https://aur.archlinux.org/packages/CLion/) support ROS packages, you can change the `Exec` parameter of its desktop file ( `~/.local/share/applications/jetbrains-clion.desktop`) as follows.

```
Exec=bash -i -c "source /home/[username]/catkin_ws/devel/setup.sh;/opt/clion/bin/clion.sh" %f

```

However, `/home/[username]/catkin_ws` must be exchanged with your Catkin workspace. You can now open a Catkin project without [cmake](https://www.archlinux.org/packages/?name=cmake) complaining about missing packages, hopefully. If desired or needed you can use Python 3 by adding `-DPYTHON_EXECUTABLE=/usr/bin/python3` to the CMake options which can be found in the settings.

## catkin build

For configuring the systems using the `catkin build` environment, one have to configure the catkin workspace as usual and issue a

```
catkin config -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so

```

Afterwards, use `catkin build` as normal. Please remember to reconfigure your catkin whenever you delete the configuration files (i.e. the `catkin_ws` directory)

## Rebuild when shared libraries are updated

When you update a library that ROS depends on (e.g. Boost), all packages that link to it must be rebuilt. Most AUR helpers will not detect this situation. The following script will generate a list of all packages that are linked to missing so files:

[https://seangreenslade.com/h/snippets/ros-find-outofdate.py](https://seangreenslade.com/h/snippets/ros-find-outofdate.py)

(Note that the script requires [pyalpm](https://www.archlinux.org/packages/?name=pyalpm) to be installed.)

## Ros 2

### Building from source

Build instructions are available at [https://index.ros.org/doc/ros2/Installation/Dashing/Linux-Development-Setup/](https://index.ros.org/doc/ros2/Installation/Dashing/Linux-Development-Setup/).

Install build dependencies: [wget](https://www.archlinux.org/packages/?name=wget), [python](https://www.archlinux.org/packages/?name=python), [python-yaml](https://www.archlinux.org/packages/?name=python-yaml), [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [git](https://www.archlinux.org/packages/?name=git), [cmake](https://www.archlinux.org/packages/?name=cmake), [asio](https://www.archlinux.org/packages/?name=asio), [tinyxml](https://www.archlinux.org/packages/?name=tinyxml), [tinyxml2](https://www.archlinux.org/packages/?name=tinyxml2), [eigen](https://www.archlinux.org/packages/?name=eigen), [libxaw](https://www.archlinux.org/packages/?name=libxaw), [glu](https://www.archlinux.org/packages/?name=glu), [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), [opencv](https://www.archlinux.org/packages/?name=opencv), [python-vcstool](https://aur.archlinux.org/packages/python-vcstool/), [python-empy](https://aur.archlinux.org/packages/python-empy/).

Fetch the sources:

```
$ mkdir -p ~/ros2_ws/src
$ cd ~/ros2_ws
$ wget [https://raw.githubusercontent.com/ros2/ros2/release-latest/ros2.repos](https://raw.githubusercontent.com/ros2/ros2/release-latest/ros2.repos)
$ vcs import src < ros2.repos

```

Presently some fixes are required:

```
$ cd ~/ros2_ws/src/ros2/rviz/
$ git remote add racko [https://github.com/racko/rviz.git](https://github.com/racko/rviz.git)
$ git fetch racko added_cmake_project_type fix_fallthrough fix_wrong_yaml_cpp
$ git cherry-pick racko/added_cmake_project_type racko/fix_fallthrough racko/fix_wrong_yaml_cpp

```

Now you can build the workspace:

```
$ cd ~/ros2_ws
$ src/ament/ament_tools/scripts/ament.py build --symlink-install

```

Read [https://github.com/ros2/ros1_bridge/blob/master/README.md#build-the-bridge-from-source](https://github.com/ros2/ros1_bridge/blob/master/README.md#build-the-bridge-from-source) regarding Ros 1 / Ros 2 interoperability.

### Usage Examples

First source the workspace:

```
$ . ~/ros2_ws/install/local_setup.bash

```

Functionality comparable to `roscore`, `rosnode`, `rostopic`, `rosmsg`, `rospack`, `rosrun` and `rosservice` is available via `ros2`:

```
$ ros2 -h
usage: ros2 [-h] Call `ros2 <command> -h` for more detailed usage. ... 

ros2 is an extensible command-line tool for ROS 2.

optional arguments:
  -h, --help            show this help message and exit

Commands:
  daemon    Various daemon related sub-commands
  msg       Various msg related sub-commands
  node      Various node related sub-commands
  pkg       Various package related sub-commands
  run       Run a package specific executable
  security  Various security related sub-commands
  service   Various service related sub-commands
  srv       Various srv related sub-commands
  topic     Various topic related sub-commands

  Call `ros2 <command> -h` for more detailed usage.

```

A typical "Hello World" example starts with running a publisher node:

```
$ ros2 topic pub /chatter 'std_msgs/String' "data: 'Hello World'"

```

Then, in another terminal, you can run a subscriber (Don't forget to source the workspace in every new terminal):

```
$ ros2 topic echo /chatter

```

List existing nodes:

```
$ ros2 node list
publisher_std_msgs_String

```

List topics:

```
$ ros2 topic list
/chatter

```

Ros 2's version of rviz is

```
$ rviz2

```