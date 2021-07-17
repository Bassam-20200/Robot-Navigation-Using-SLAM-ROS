# Robot-Navigation-Using-SLAM-ROS

**This Repository will explain my 2nd task in Robotics and AI department at SMART METHODS summer training.**

## Task Requirements: 
  * Use [Turtlebot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/#overview) (ROS standard platform robot) with SLAM approach (simultaneous localization and mapping) to creat a map using Lidar sensor and then save the map. 

## Detailed Steps:
 1. we start this task, I installed Ubuntu 18.04 and ROS Melodic with Gazebo and Rviz Simulator ([see my repo](https://github.com/mo7ammed-saleh/Robot_Arm_Control_in_ROS/blob/main/README.md)). Now, I will Install ROS 1 on Remote PC using the following comand
    -  `sudo apt update`
    -  `sudo apt upgrade`
    -  `wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh`
    -  `chmod 755 ./install_ros_melodic.sh `
    -  `bash ./install_ros_melodic.sh`
 2. Install Dependent ROS 1 Packages
    - `sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy \
  ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc \
  ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan \
  ros-melodic-rosserial-arduino ros-melodic-rosserial-python \
  ros-melodic-rosserial-server ros-melodic-rosserial-client \
  ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server \
  ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro \
  ros-melodic-compressed-image-transport ros-melodic-rqt* \
  ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers`
  
  3. Install TurtleBot3 Packages
     - ` sudo apt-get install ros-melodic-dynamixel-sdk`
     - `sudo apt-get install ros-melodic-turtlebot3-msgs` 
     - `sudo apt-get install ros-melodic-turtlebot3`
 4. Install Simulation Package where the TurtleBot3 Simulation Package requires turtlebot3 and turtlebot3_msgs packages as prerequisite. Without these prerequisite packages, the Simulation cannot be launched.
    - `cd ~/catkin_ws/src/`
    - `git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git`
    - `cd ~/catkin_ws && catkin_make`
    - Then write `cd` or open new terminal and write `source ~/catkin_ws/devel/setup.bash` or use `echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc`
 

 5. Launch Simulation World.There are 3 simulation environments are prepared for TurtleBot3 and I will lunch one by one just for testing (we can choose one of them later).
   - Empty world with a robot called "burger" 
     - `export TURTLEBOT3_MODEL=burger`
     - `roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch`
     - 
     
   - TurtleBot3 World with a robot called "waffle"
     - `export TURTLEBOT3_MODEL=waffle`
     - `roslaunch turtlebot3_gazebo turtlebot3_world.launch`
     -  

      
   - TurtleBot3 House with a robot called waffle_pi
      - `export TURTLEBOT3_MODEL=waffle_pi`
      - `roslaunch turtlebot3_gazebo turtlebot3_house.launch`
      -  
      
      
6. We will choose one of the previous robot which is waffle and we weill cintrol it usit the keybored keys  W: Forward,  A: Left, S:Stop, D: Right, X:Backward. So, Run the previous comand for waffle robot then open new terminal and run the following command:
   - `roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch` 

______________________________________________________________________________________________________________________
7. **Now**, close everthing and lets use SLAM simulation to creat the a map for our world, and then save the map with help of lidar sensor. There are 3 Gazebo environments are prepared as mentioned in step 5, but for creating a map with SLAM, it is recommended to use either TurtleBot3 World or TurtleBot3 House. So, I will use TurtleBot3 World with a robot called "waffle" to creat the map and save it.

   - Lunch the Gazebo environment with waffle robot `export TURTLEBOT3_MODEL=waffle` then `roslaunch turtlebot3_gazebo turtlebot3_world.launch`
   - Open new terminel to Run SLAM Node `export TURTLEBOT3_MODEL=waffle` then `roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping`
   - Open a new terminal to control the waffel robot and scan the area using lidar sensor `export TURTLEBOT3_MODEL=waffle` then ` roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch`. (in the terminal we will control the robot direction using W,A,S,D,X keybored keys).
  
   - 8. When the map is created successfully in Rviz, open new terminal and save it using the command `rosrun map_server map_saver -f ~/map` 


    ![img 1](https://user-images.githubusercontent.com/54133895/126042220-e9ff8bf3-6df9-48ad-bc5b-f013925859c0.png)
![img 2](https://user-images.githubusercontent.com/54133895/126042221-7081b3f8-319b-4a34-961c-d7d616004822.png)
![img 3](https://user-images.githubusercontent.com/54133895/126042222-d40ba7ea-6cfd-441b-8000-7ad245c06943.png)
![img 4](https://user-images.githubusercontent.com/54133895/126042224-41b106a5-be1a-42c5-a3f1-4d79c12bc878.png)
![img 5](https://user-images.githubusercontent.com/54133895/126042225-74085c5b-3c6f-4391-b5d4-ed7d818ddf99.png)

   
