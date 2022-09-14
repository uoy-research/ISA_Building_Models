# Blender and Gazebo (classic) Models of the ISA Building
This repository links to files containing models of the ISA Building for both Blender and Gazebo.  
The models were created by Tom Feilden supervised by Victoria Hodge and James Walker in collaboration with Richard Hawkins and Matt Osborne for a Venables Internship 2022.  
The models are available under a CC-BY-SA-4.0 licence - see the LICENSE file in the repo for details. You can distribute, remix, adapt, and build upon the material in any medium or format, so long as attribution is given to the creators.

- The Blender models require 

  * [Blender **version 300.43** or newer](https://www.blender.org/).

    * If the model appears black when imported into Blender then check the Blender version.
    
    * If parts of the model are coloured pink/purple then the necessary image files may not have imported correctly. These imports can be checked by going to  
    `File->External Data->Report Missing Files` and viewing the resulting log. 

- The Gazebo models require 

  * [Ubuntu 20.04 LTS](https://releases.ubuntu.com/20.04/)

  * [ROS 2 - Galactic](https://docs.ros.org/en/foxy/Releases/Release-Galactic-Geochelone.html)

  * [Gazebo 11.1.0](http://gazebosim.org/)

## Blender

Blender models can be exported to a number of simulation environments suitable for robotics and autonomous systems. We have exported to Gazebo but, by downloading and exporting the Blender models, other simulation models can be created.

![Blender models can be exported to Gazebo, Nvidia Isaac, Unity3D or other models](Drawing1.jpg "Models (showing available models in green)")

The following ISA Building Blender models are available:

- ISA Building Ground Floor [Download Blender Model here - XXX MB]()

- ISA Building [Download Blender Model here - XXX MB]()

- Test Space 2 [Download Blender Model here - 39 MB](https://drive.google.com/file/d/1U4kwkS-2b2KzH41lF9wv7h92EtZNj0s3/view?usp=sharing)

## Gazebo

---
# Setting-up-a-world-in-Gazebo - by Tom Feilden
All the details (and unique quirks) that I found out during my Summer Internship

## Prerequisites: ##
* [ROS2 Galactic](https://automaticaddison.com/how-to-install-ros-2-foxy-fitzroy-on-ubuntu-linux/) installed on Ubuntu Linux 20.04
    * _Note: this tutorial is designed for Ros2 Foxy so replace all "__foxy__"  with "__galactic__"_
* You have [created a ROS 2 workspace](https://automaticaddison.com/how-to-create-a-workspace-ros-2-foxy-fitzroy/) (I had "__dev_ws__")
* Python 3.7 installed
* You have a package named __two_wheeled_robot__ inside __~/dev_ws/src__
    * From this [tutorial](https://automaticaddison.com/how-to-load-a-urdf-file-into-rviz-ros-2/)


## Useful Resources ##
A very useful series of websites is made by AutomaticAddison. Some of the sections in the website is out of date so take all the files from [their Github](https://github.com/automaticaddison/two_wheeled_robot)

If in doubt:
* StackOverflow
* Gazebo Answers
* ROS Answers

## Adding a custom model to Gazebo: ##
### Option 1 ###
__Follow these steps first. Only go to option 2 if you can't save the Gazebo world__
1. Load up gazebo (in verbose mode you can find any errors that come up)

    `gazebo --verbose`
    
2. Go to Edit -> Model Editor (Ctrl + M)
3. Go to Custom Shapes and click add
4. Then browse for the model you want to add 

      _This will be a collada (.dae) file_
  
      __Make sure the collada file is in a folder with all the textures required__

5. Place your model in the world and save the model
6. To change the model from grey to the textures you added:
    1. Go to your file manager and go to the folder __model_editor_models__
    2. Find the folder corresponding to the model name you just saved
    3. Open the __model.sdf__
    4. Delete this seciton of code:
    
     ```
        <material>
          <lighting>1</lighting>
          <script>
            <uri>file://media/materials/scripts/gazebo.material</uri>
            <name>Gazebo/Grey</name>
          </script>
          <shader type='pixel'/>
        </material>
    ```
7. Delete the model from your world
8. Insert the model (from the insert tab)
9. Repeat these steps until you have created your desired world 
10. To save the world, go to File -> Save World As (Ctrl + shift + s)

### Option 2 ###
__If you encounter an issue where you can't save your gazebo world, follow these steps__
1. Load up Gazebo using sudo

        `sudo gazebo --verbose`
        
2. Follow steps 2 - 5 in __Option 1__
3. To change the model from grey to the textures you added:
    1. Open a new terminal and type:

    `sudo nautilus`
    
    2. Find the folder corresponding to the model name you just saved
    3. Open the __model.sdf__
    4. Delete this seciton of code:
    
     ```
        <material>
          <lighting>1</lighting>
          <script>
            <uri>file://media/materials/scripts/gazebo.material</uri>
            <name>Gazebo/Grey</name>
          </script>
          <shader type='pixel'/>
        </material>
    ```
4. Delete the model from your world
5. Insert the model (from the insert tab)
6. Repeat these steps until you have created your desired world 
7. To save the world, go to File -> Save World As (Ctrl + shift + s)
  
## Make a world ##

1. Open Gazebo
2. Add what ever models to your world that you would like
3. Save the model in thee __two_wheeled_robots/worlds__ folder 
4. Open up that file and paste this section of code at the end just above __</world>__:
   ```  
   <include>
    <uri>model://two_wheeled_robot_description</uri>
    <static>false</static>
    <pose>-20.0 4.0 3.5 0 0 0</pose>
   </include> 
   ```
  
   
## How to launch the world ##

1. Creating the launch file

    `colcon_cd two_wheeled_robot`

    `cd launch`

    `gedit load_world_into_gazebo.launch.py`
2. Add the code from the [load_world_into_gazebo.launch.py](https://github.com/Piebee007/Setting-up-a-world-in-Gazebo/blob/main/load_world_into_gazebo.launch.py/ "load_world_into_gazebo.launch.py") file which is in the repository
3. Change line 24 from 
    `world_file_name = 'CHANGE_ME.world'`
    to the name of your world
4. Save the file and close it
5. Go to your root directory

    `cd ~/dev_ws`
    
6. Build the package

    `colcon build`
    
7. Open a new terminal  and run the launch file using this command:

    `ros2 launch two_wheeled_robot load_world_into_gazebo.launch.py`
    
    
    
## Creating a map for RVIZ ##
Creating a map for rviz involves taking a picture of the floor plan (either .png or .jpeg) and outputs a .pmg and a .yaml file which sets the scale of the map

__BE AWARE:__ door diagrams and other marks in the picture will be perceived as a wall. Use software like paint to remove the unnecessary information

1. Add the files needed which is in the _maps_ folder in the root directory 
    1. Add the file [convert_to_binary.py](https://github.com/Piebee007/Setting-up-a-world-in-Gazebo/blob/main/convert_to_binary.py)
    2. Add the file [MakeROSMap.py](https://github.com/Piebee007/Setting-up-a-world-in-Gazebo/blob/main/MakeROSMap.py)
  
2. Change the file names in the "__convert_to_binary.py__" indicated by the __CHANGE_ME__

3. Convert the floorplan to binary and then make the ros map

    To run code do `python3 *insert file name here*` in a terminal
    
    Follow the prompts  in the terminal
    
4. Edit the .yaml file kjhdsakjhsakjdhfkjsdhgkjsfkjheksjfhkjhkjdhksjhkjhkjhkjhkjkjhkjhkjh
    
    
    
## Launch RVIZ ##

### Editing the launch file: ###
Change the file names in the [launch file](https://github.com/Piebee007/Setting-up-a-world-in-Gazebo/edit/main/isa_world_v1.launch.py)
``` py
def generate_launch_description():
  package_name = 'two_wheeled_robot'
  robot_name_in_model = 'two_wheeled_robot'
  default_launch_dir = 'launch'
  gazebo_models_path = 'models'
  map_file_path = 'maps/CHANGE_ME.yaml'
  nav2_params_path = 'params/CHANGE_ME/nav2_params.yaml'
  robot_localization_file_path = 'config/ekf.yaml'
  rviz_config_file_path = 'rviz/CHANGE_ME/nav2_config.rviz'
  sdf_model_path = 'models/two_wheeled_robot_description/model.sdf'
  urdf_file_path = 'urdf/two_wheeled_robot.urdf'
  world_file_path = 'worlds/CHANGE_ME.world'

```
### Launching ###

__Note:__ After any edit of any file, you must rebuild the file

1. Open a new terminal and go to the root directory and build the files

    `cd ~/dev_ws`
    
    `colcon build`
    
2. Open another new terminal and type in this command:

    `ros2 launch two_wheeled_robot *insert_launch_file_name*.launch.py`
 
    
    
### Setting up the Camera ###
Assumption that the two_wheeled_robot 's .sdf and .udrf has been set up for using a camera

1. Click on the button "__ADD__" which is on the left of the screen
2. Go to __By topic -> /depth camera/ image__ and click __OK__
3. Find the __image__ in the Display section (on the left of the screen)
4. Go to __Topic -> Reliaility Pollicy__ and change from "__Reliable__" to "__Best Effort__"

*Note: You can drag the image section out of  the rviz window to have a seperate window of what the robot camera is seeing*


### Moving the robot ###

To install the the package type this command:

`sudo apt-get install ros-galactic-rqt-robot-steering`

Then open a new terminal and to run the program type this command:

`rqt_robot_steering`

You can either interact with the GUI with your __mouse__ or using __WASD__ to move the robot.

*Note: Having the camera set up makes moving the robot around a lot easier*
