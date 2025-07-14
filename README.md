# Introduction  
- **px4_sim** is a ros1 package that uses PX4-SITL with gazebo classic (v11) and MAVROS for controlling the drone.   
- The steps have been mentioned to install and build this project from scratch.   

## Platform configuration   
- Ubuntu-20.04 LTS Desktop
- ROS-Noetic
- Gazebo Classic v11 

## Install and build PX4 SITL

- Clone px4 autopilot and install dependencies  

    ```bash
    cd ~
    git clone https://github.com/PX4/PX4-Autopilot.git --recursive  
    bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
    ```

- Build the px4 sitl configuration    

    ```bash
    cd ~/PX4-Autopilot
    make px4_sitl gazebo-classic
    ```

- Add the following directory to path

    ```bash
    export PATH="$HOME/.local/bin:$PATH"
    ```

- You can use following commands on the PX4 SITL terminal to  

    takeoff the drone

    ```bash
    commander takeoff
    ```    

    land the drone  

    ```bash
    commander land
    ```  

## Install QGroundControl (base station)  

- Official instructions for installing QGroundControl are on [docs.qgroundcontrol.com](https://docs.qgroundcontrol.com/Stable_V4.3/en/qgc-user-guide/getting_started/download_and_install.html).   

- The steps are as follows   

    ```bash
    sudo usermod -a -G dialout $USER
    sudo apt-get remove modemmanager -y
    sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
    sudo apt install libqt5gui5 -y
    sudo apt install libfuse2 -y
    ```  

- Logout and login again to enable the change to user permissions.  

- Download [QGroundControl.AppImage](https://d176tv9ibo4jno.cloudfront.net/latest/QGroundControl.AppImage) in your home directory.  

- Install and run QGroundControl  

    ```bash
    cd ~
    chmod +x ./QGroundControl.AppImage
    ./QGroundControl.AppImage
    ```  

## Install MAVROS and its dependencies

- Binally installation for mavros  

    ```bash
    sudo apt-get install ros-${ROS_DISTRO}-mavros ros-${ROS_DISTRO}-mavros-extras ros-${ROS_DISTRO}-mavros-msgs
    ```  

- Install [GeographicLib](https://geographiclib.sourceforge.io/) dataset  

    ```bash
    wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
    sudo bash ./install_geographiclib_datasets.sh
    ```

-   Paste the following in your *.bashrc* file so that ros can find path to **px4** packages

    ```bash
    source ~/PX4-Autopilot/Tools/simulation/gazebo-classic/setup_gazebo.bash ~/PX4-Autopilot ~/PX4-Autopilot/build/px4_sitl_default
    export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4-Autopilot
    export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/PX4-Autopilot/Tools/simulation/gazebo-classic/sitl_gazebo-classic        
    ```