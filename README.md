<!--
*** Merci d'avoir consulté le modèle Best-README. Si vous avez une suggestion
*** pour amelioré notre projet portant sur un robot mobile
*** cett partie vous parle de la cartagraphie, navigation et detsction des obstacles avec le RPLIDAR et ROS sous RPI4.
*** LE GROUPS LIDAR VOUS REMERCIE! :D

-->

## Author

👤**NIANE ABDOULAYE** [🇫🇷 Contactez moi](<ablayeniane658@gmail.com>)

***
# 📎 PGE_MASTER_2_SME_RPLIDAR_GROUPS :  Creating a README file for GitHub

![left 100%](images/rpilidar.jpg?raw=true)

_`Project start date 22/10/2021`_

<!-- LOGO DU PROJET -->
<br />
<p align="center">

<!-- TABLE DES MATIÈRES -->
<details open="open">
  <summary><h2 style="display: inline-block">Table des matières</h2></summary>
  <ol>
    <li>
      <a href="#a-propos-du-projet">About the project</a>
      <ul>
        <li><a href="#construit-avec">Construit avec</a></li>
      </ul>
    </li>
    <li>
      <a href="#connect-your-rplidar">Connect your RPLIDAR</a>
      <ul>
        <li><a href="#conditions-préalables">Prerequisites</a></li>
      </ul>
    </li>
    <li><a href="#Workspace-configuration-and-installation-of-RPLIDAR-ROS-packages">Workspace configuration and installation of RPLIDAR ROS packages</ a></li>
    <li><a href="#feuille-de-route">Feuille de route</a></li>
    <li><a href="#launch-of-the-project">Launch of the project</a>
      <ul>
        <li><a href="#conditions-préalables">Run the RPLIDAR launch file</a></li>
        <li><a href="#rviz">rviz</a></li>
      </ul></li>
    <li><a href="#contribution">Contribution</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#remerciements">Remerciements</a></li>
  </ol>
</details>

<!-- A PROPOS DU PROJET -->
## A propos du projet

Il existe de nombreux modèles de README sur GitHub, mais je n'en ai pas trouvé un qui réponde vraiment à mes besoins, alors j'ai créé ce modèle amélioré.

Bien sûr, il n'existe pas de modèle unique pour tous les projets, car vos besoins peuvent être différents. Vous pouvez suggérer des changements en créant une demande de modification ou en ouvrant un problème. Merci à toutes les personnes qui ont contribué à l'expansion de ce modèle !

Une liste de ressources couramment utilisées et que je trouve utiles est listée dans les remerciements.

# RPLIDAR_GROUPS
## Connect your RPLIDAR
#### Prerequisites
#### Open a terminal and verify permissions
```
ls -l /dev | grep ttyUSB
sudo chmod 666 /dev/ttyUSB0
```

#### Update the list of packages
```
sudo apt-get update
```
#### Installation of dependencies
```
sudo apt-get install gedit
```

## Workspace configuration and installation of RPLIDAR ROS packages
#### Installation of dependencies
```
sudo apt-get install cmake python-catkin-pkg python-empy python-nose python-setuptools libgtest-dev python-rosinstall python-rosinstall-generator python-wstool build-essential git
```
#### Creation de l'espace de travail Catkin
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
```
#### Modify the file .bashrc
```
gedit ~/.bashrc
```
#### Put these two lines at the end of the .bashrc file
```
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash
```
#### Save the file.

#### Type this command on the current terminal
```
source ~/catkin_ws/devel/setup.bash
```
#### Go to the src folder
```
cd src
```
#### Clone the project into your src folder
```
lien clone à mettre ici
```
#### Open this file
```
cd ~/catkin_ws/src/rplidar_ros/src
```
#### Change the permissions
```
sudo chmod +x node.cpp
```
#### Go to the workspace
```
cd ~/catkin_ws/
```
#### Compile the project
```
catkin_make
```

### Launch of the project
```
#### Run the RPLIDAR launch file
```
roslaunch rplidar_ros rplidar.launch
```
#### Open a new terminal to see the list of topics
```
rostopic list
```
#### Open a new terminal
```
rostopic echo /scan
```
#### Warning! keep the terminal open for the next section
```
#### rviz
#### Open a new terminal and run rviz
```
rviz
```
#### Once the rviz window appears
```
#### Put
```
Fixed Frame = laser
```
#### Click on the bottom left of the window on add and select LaserScan then click on OK
```
#### Put
```
LaserScan = /scan
```
#### You can increase the size for a better visualization of the data
```
size(m) = 0.04
```
#### To close the terminal press CTRL+C


## Creating a map using the Hector-SLAM ROS package
```
#### Installing Qt4
```
sudo apt-get install qt4-qmake qt4-dev-tools
```
#### Update the packages
```
sudo apt-get update
```
#### Open this file
```
cd ~/catkin_ws/src/hector_slam
```
#### Open a new terminal 
```
cd ~/catkin_ws/
```
#### Compile the package
```
catkin_make
```
#### If you see an error message of type
```
Project ‘cv_bridge’ specifies ‘/usr/include/opencv’ as an include dir, which is not found. It does neither exist as an absolute directory nor in....
```
#### Enter 
```
cd /usr/include
sudo ln -s opencv4/ opencv
```
#### Compile the package
```
cd ~/catkin_ws/
catkin_make
```
#### Reboot your computer
```
sudo shutdown -h now
```

### Launch of the mapping
```
#### Open a new terminal and start RPLIDAR
```
cd ~/catkin_ws/
sudo chmod 666 /dev/ttyUSB0
roslaunch rplidar_ros rplidar.launch
```
#### Now that the LIDAR is running, let's start the mapping
```
#### Open a new terminal
```
roslaunch hector_slam_launch tutorial.launch
```
#### You can move the LIDAR very slowly around the room to get a good map

#### Save the Map
```
### Using the map_server method to register the map
```
#### Installing map_server
```
sudo apt-get install ros-kinetic-map-server
```
#### Create the folder for the map
```
mkdir ~/catkin_ws/maps
```
#### Start the mapping process (see the section Starting the mapping above)
```
#### Open a new terminal
```
cd ~/catkin_ws/maps
rosrun map_server map_saver -f my_map_rplidar_ros
```
#### The map will be saved in the ~/catkin_ws/maps directory in yaml and pgm format
```
#### Type CTRL+C to close the terminal
```

### Load the registered map
```
#### Open a new terminal
```
cd ~/catkin_ws/maps
roscore
```
#### Load the map with the command
```
rosrun map_server map_server my_map_rplidar_ros.yaml
```
#### Open rviz in a new terminal
```
rviz
```
#### Press the add button at the bottom left and add Map
```
#### Set Topic = /map
```
#### You should see your map on rviz
```

### Convert your map to png format
```
#### Install the package
```
sudo apt-get install imagemagick
convert my_map_rplidar_ros.pgm my_map_rplidar_ros.png
```

### Edit map
```
#### Install gimp
```
sudo apt-get update
sudo apt-get install gimp
```
#### Launch gimp
gimp
```
#### To load the image, go to File -> Open , then locate your image
```
### Customize configuration
#### See [Configuration Reference]
```
https://automaticaddison.com/how-to-build-an-indoor-map-using-ros-and-lidar-based-slam/
```
# PGE_MASTER_2_SME_2022_RPLIDAR_GROUPS











