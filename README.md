# Turtlebot3_Maze_Navigator


# Abstract

The robot is trapped in a maze and must escape it. We use SLAM and NAV2 to help the bot navigate.
We are using the URDF model of the turtlebot3 for this purpose.


![Screenshot 2024-09-26 194318](https://github.com/user-attachments/assets/d3a145ab-8721-410f-94ff-371af00128d3)







# Requirements
The ROS packages of turtlebot3, Cartographer and Nav2 are required.

For example, you can install Cartographer on  Ubuntu 22.04.4 LTS by the following command:<br>
   
        sudo apt install ros-humble-cartographer 

for Nav2-
        
        sudo apt install ros-humble-cartographer 

Clone the git files of turtlebot3 in a new workspace using-

        git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
    




# Repository architecture
## Directories
* maze_runner/
  
  * launch/ :  contains launch file for starting the simulation / running of the model in gazebo
  * map/ :  contains the map generated using cartographer and SLAM
  * worlds/ :  contains the world to be loaded in Gazebo

   



# Direct usage
* Clone this repository into a ROS catkin workspace
* Build and source the workspace
* To view this robot model on Gazebo:





        ros2 launch turtlebot3_gazebo turtlebot3_maze.launch.py
  

  

# Navigation

## Generate the map of the maze using cartographer
Control the robot inside Gazebo by launching it using the following launch file:

    ros2 launch turtlebot3_gazebo turtlebot3_maze.launch.py

This will launch the turtlebot3 in gazebo.

In another terminal start the cartographer launch file-

    ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True

This will open Rviz2 where you will be able to see the local and global costmaps.

To control the turtlebot3 in gazebo and generate the map use-

    ros2 run turtlebot3_teleop teleop_keyboard

Now create the map by moving the bot around till there is not so much grey area left.

## To save the generated map

To save the map generated using the cartographer-

    ros2 run nav2_map_server map_saver_cli -f map/maze

To fix the map install gimp-

    sudo apt install gimp

Open gimp and open the map and fix all the boundaries to make sure the bot does not escape through them

![Screenshot 2024-09-26 200451](https://github.com/user-attachments/assets/fe66e462-9e95-4b3d-8d97-4569822cff1b)



## To Navigate the robot in the maze
Start the robot in gazebo-

      ros2 launch turtlebot3_gazebo turtlebot3_maze.launch.py

Start in a different terminal the navigation-

      ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=map/maze.yaml

This will start Rviz along with the generated map
      

![Screenshot 2024-09-26 200843](https://github.com/user-attachments/assets/953b21a3-054d-4a30-a0bc-575c70c0d6f8)

Using the 2d pose estimate input the initial pose of the robot, you will be able to see the global and local costmap.

Using the select goal option , you cana select the exit of the maze and the robot will navigate its way to the exit.

Alternatively , you can also input the waypoints and the initial pose through a python scrip and interact programmatically with nav2.








https://github.com/user-attachments/assets/cd494371-a587-467e-a2d2-7283d69f3a47








  
