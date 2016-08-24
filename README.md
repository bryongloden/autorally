# AutoRally

![alt text](doc/autorally_repo.jpg "Platform image")

Software for the AutoRally research platform.

[AutoRally Platform Website](http://autorally.github.io)

[AutoRally Youtube Channel](https://www.youtube.com/channel/UCSt0P1uqi4zU5RX2DZC_Qvg)

Research Pages AutoRally is associated with:
  * http://rehg.org/autorally
  * http://dcsl.gatech.edu/research-muri-nascar.html
  * http://acds-lab.gatech.edu/Research.html

## Contributing

We welcome bug fixes, ehancements, new features, and [feedback](https://github.com/AutoRally/autorally/issues)!

Please submit pull requests to the [devel branch](https://github.com/AutoRally/autorally/pull/new/devel) that conform to the [ROS C++ Style Guide](http://wiki.ros.org/CppStyleGuide). We use Gitflow, so master branch is reserved for releases.

## Setup Instructions

### Contents
1. [Install Prerequisites](#1-install-prerequisites)
2. [Clone repository](#2-clone-or-fork-repositories)
3. [Install AutoRally ROS Dependencies](#3-install-autorally-ros-dependencies)
4. [Compilation/Running](#4-compilation-running)
5. [Generate Documentation](#5-generate-documentation)
6. [Test Setup in Simulation](#6-test-setup-in-simulation)

### 1. Install Prerequisites
1. __Install [Ubuntu 14.04 64-bit](http://www.ubuntu.com)__
2. __Install required packages__

   ```sudo apt-get install git doxygen openssh-server libusb-dev texinfo```
   
   _Recommended Tools_
   
   The following tools are useful, but not necessary for this project.
   * feh
   * cutecom
   * cmake-curses-gui
   * coriander
   * synaptic
   * arduino
   * python-termcolor
   
3. __[Install](http://www.ros.org/install/) ros-indigo-desktop-full__
4. __Install gtsam__

   Follow the gtsam [Quick Start](https://bitbucket.org/gtborg/gtsam/) guide to clone and install the _develop_ branch of gtsam. 

   Instead of `cmake ..`, use:

   ```cmake -DGTSAM_INSTALL_GEOGRAPHICLIB=ON -DGTSAM_WITH_EIGEN_MKL=OFF ..```

   Once install is complete, make sure linux can see the shared library:

   ```sudo ldconfig```
   
### 2. Clone or Fork Repositories

Get the autorally and imu_3dm_gx4 repositories in a [catkin workspace](http://wiki.ros.org/catkin/workspaces). The suggested location is `~/catkin_ws/src/`, but any valid catkin worskspace source folder will work. We suggest forking if you will be working with the code.

To clone:

    git clone https://github.com/AutoRally/autorally.git
    git clone https://github.com/AutoRally/imu_3dm_gx4.git

### 3. Install AutoRally ROS Dependencies

Within the catkin workspace folder, run this command to install the packages this project depends on.

```rosdep install --from-path src --ignore-src -y```

### 4. Compilation & Running

To compile and install run `catkin_make` from the catkin workspace folder.

Due to the additional requirement of ROS's distributed launch system, you must run

`source src/autorally/autorally_util/setupEnvLocal.sh`

before using any AutoRally components. See the [wiki](https://github.com/AutoRally/autorally/wiki) for more information about how to set this system up for distributed launches on your vehicle platform.

_Note:_ If you are unfamiliar with catkin, please know that you must run `source <catkin_ws>/devel/setup.sh` before ROS will be able to locate the autorally packages. This line can be added to your ~/.bashrc file.

### 5. Generate Documentation

You can generate / update code documentation by running `doxygen` in `autorally/`.

To view code documentation open `autorally/doc/html/index.html` in a web browser.

### 6. Test Setup in Simulation

To test that your setup process was successful, run the AutoRally simulator with the following command. You can use a USB gamepad to drive the simulated platform around. On startup, the `runstop` message published by the joystick node is false. Press any of the buttons by the right stick (normally labelled X, Y, A, B or square, triangle, X, circle) to toggle the published value.

If you do not have a gamepad and want to control the platform autonomously in simulation, comment out the joystick node launch line in the simulation launch file so that it doesn't publish a `runstop` message that is always false.
 
```roslaunch autorally_gazebo autoRallyTrackGazeboSim.launch```

## What's Next

Check out the [wiki](https://github.com/AutoRally/autorally/wiki) for:
* Instructions to configure a physical AutoRally platform
* Tutorials for released controllers (waypoint follower, constant speed controller)
* Tutorial to use your own controller with the AutoRally platform
* Information about how to run the included state estimator
