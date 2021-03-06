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
*   [6 ROS 2](#ROS_2)
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

As specified by the [ROS wiki](http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment), the first catkin_make command in a clean workspace should be:

```
catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYTHON_INCLUDE_DIR=/usr/include/python3.7m -DPYTHON_LIBRARY=/usr/lib/libpython3.7m.so

```

Subsequent builds should be done with just

```
catkin_make

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

## ROS 2

### Building from source

Build instructions are available at [https://index.ros.org/doc/ros2/Installation/](https://index.ros.org/doc/ros2/Installation/).

Install build dependencies.

Dependencies for Eloquent: (official packages in alphabetical order; AUR packages in an order in which you can sequentially install them without dependency errors) The [ros2-arch-deps](https://aur.archlinux.org/packages/ros2-arch-deps/) package attempts to address this, but is out of date. It might be recommended to modify its PKGBUILD manually for now so that these dependencies can be removed altogether when uninstalling ROS 2. [asio](https://www.archlinux.org/packages/?name=asio) [cmake](https://www.archlinux.org/packages/?name=cmake) [eigen](https://www.archlinux.org/packages/?name=eigen) [glew](https://www.archlinux.org/packages/?name=glew) [git](https://www.archlinux.org/packages/?name=git) [glu](https://www.archlinux.org/packages/?name=glu) [hdf5](https://www.archlinux.org/packages/?name=hdf5) [libxaw](https://www.archlinux.org/packages/?name=libxaw) [opencv](https://www.archlinux.org/packages/?name=opencv) [poco](https://www.archlinux.org/packages/?name=poco) [python](https://www.archlinux.org/packages/?name=python) [python-cryptography](https://www.archlinux.org/packages/?name=python-cryptography) [python-lark-parser](https://www.archlinux.org/packages/?name=python-lark-parser) [python-netifaces](https://www.archlinux.org/packages/?name=python-netifaces) [python-nose](https://www.archlinux.org/packages/?name=python-nose) [python-numpy](https://www.archlinux.org/packages/?name=python-numpy) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5) [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools) [python-sip](https://www.archlinux.org/packages/?name=python-sip) [python-yaml](https://www.archlinux.org/packages/?name=python-yaml) [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) [sip](https://www.archlinux.org/packages/?name=sip) [tinyxml](https://www.archlinux.org/packages/?name=tinyxml) [tinyxml2](https://www.archlinux.org/packages/?name=tinyxml2) [vtk](https://www.archlinux.org/packages/?name=vtk) [wget](https://www.archlinux.org/packages/?name=wget) [log4cxx](https://www.archlinux.org/packages/?name=log4cxx) [python-empy](https://aur.archlinux.org/packages/python-empy/) [python-notify2](https://aur.archlinux.org/packages/python-notify2/) [python-pytest-repeat](https://aur.archlinux.org/packages/python-pytest-repeat/) [python-vcstool](https://aur.archlinux.org/packages/python-vcstool/) [python-colcon-argcomplete](https://aur.archlinux.org/packages/python-colcon-argcomplete/) [python-colcon-bash](https://aur.archlinux.org/packages/python-colcon-bash/) [python-colcon-catkin_pkg](https://aur.archlinux.org/packages/python-colcon-catkin_pkg/) [python-colcon-cmake](https://aur.archlinux.org/packages/python-colcon-cmake/) [python-colcon-core](https://aur.archlinux.org/packages/python-colcon-core/) [python-colcon-defaults](https://aur.archlinux.org/packages/python-colcon-defaults/) [python-colcon-devtools](https://aur.archlinux.org/packages/python-colcon-devtools/) [python-colcon-library-path](https://aur.archlinux.org/packages/python-colcon-library-path/) [python-colcon-metadata](https://aur.archlinux.org/packages/python-colcon-metadata/) [python-colcon-notification](https://aur.archlinux.org/packages/python-colcon-notification/) [python-colcon-output](https://aur.archlinux.org/packages/python-colcon-output/) [python-colcon-package-information](https://aur.archlinux.org/packages/python-colcon-package-information/) [python-colcon-package-selection](https://aur.archlinux.org/packages/python-colcon-package-selection/) [python-colcon-pkg-config](https://aur.archlinux.org/packages/python-colcon-pkg-config/) [python-colcon-parallel-executor](https://aur.archlinux.org/packages/python-colcon-parallel-executor/) [python-colcon-powershell](https://aur.archlinux.org/packages/python-colcon-powershell/) [python-colcon-python-setup-py](https://aur.archlinux.org/packages/python-colcon-python-setup-py/) [python-colcon-recursive-crawl](https://aur.archlinux.org/packages/python-colcon-recursive-crawl/) [python-colcon-ros](https://aur.archlinux.org/packages/python-colcon-ros/) [python-colcon-test-result](https://aur.archlinux.org/packages/python-colcon-test-result/) [python-colcon-zsh](https://aur.archlinux.org/packages/python-colcon-zsh/) [python-colcon-common-extensions](https://aur.archlinux.org/packages/python-colcon-common-extensions/) [python-rospkg](https://aur.archlinux.org/packages/python-rospkg/) [python-rosdistro](https://aur.archlinux.org/packages/python-rosdistro/) [python-rosdep](https://aur.archlinux.org/packages/python-rosdep/)

Dependencies for Dashing: [wget](https://www.archlinux.org/packages/?name=wget), [python](https://www.archlinux.org/packages/?name=python), [python-yaml](https://www.archlinux.org/packages/?name=python-yaml), [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [sip](https://www.archlinux.org/packages/?name=sip), [python-sip](https://www.archlinux.org/packages/?name=python-sip), [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5), [git](https://www.archlinux.org/packages/?name=git), [cmake](https://www.archlinux.org/packages/?name=cmake), [asio](https://www.archlinux.org/packages/?name=asio), [tinyxml](https://www.archlinux.org/packages/?name=tinyxml), [tinyxml2](https://www.archlinux.org/packages/?name=tinyxml2), [eigen](https://www.archlinux.org/packages/?name=eigen), [libxaw](https://www.archlinux.org/packages/?name=libxaw), [glu](https://www.archlinux.org/packages/?name=glu), [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), [opencv](https://www.archlinux.org/packages/?name=opencv), [hdf5](https://www.archlinux.org/packages/?name=hdf5), [vtk](https://www.archlinux.org/packages/?name=vtk), [glew](https://www.archlinux.org/packages/?name=glew), [poco](https://www.archlinux.org/packages/?name=poco), [python-nose](https://www.archlinux.org/packages/?name=python-nose), [python-numpy](https://www.archlinux.org/packages/?name=python-numpy), [python-lark-parser](https://www.archlinux.org/packages/?name=python-lark-parser), [python-cryptography](https://www.archlinux.org/packages/?name=python-cryptography), [python-netifaces](https://www.archlinux.org/packages/?name=python-netifaces), [python-vcstool](https://aur.archlinux.org/packages/python-vcstool/), [python-empy](https://aur.archlinux.org/packages/python-empy/), [log4cxx](https://www.archlinux.org/packages/?name=log4cxx), [python-colcon-common-extensions](https://aur.archlinux.org/packages/python-colcon-common-extensions/), [python-rosdep](https://aur.archlinux.org/packages/python-rosdep/).

Fetch the sources:

```
$ mkdir -p ~/ros2_ws/src
$ cd ~/ros2_ws
$ wget [https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos](https://raw.githubusercontent.com/ros2/ros2/master/ros2.repos)
$ vcs import src < ros2.repos

```

Note: Replace "master" with whatever distribution is desired (e.g. "dashing").

Now you can build the workspace:

```
$ cd ~/ros2_ws
$ colcon build --symlink-install

```

Read [https://github.com/ros2/ros1_bridge/blob/master/README.md#build-the-bridge-from-source](https://github.com/ros2/ros1_bridge/blob/master/README.md#build-the-bridge-from-source) regarding ROS 1 / ROS 2 interoperability.

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

ROS 2's version of rviz is

```
$ rviz2

```