# pepperTeleoperation

System requirement<br>
  Ubuntu 14.04<br>
  ROS Indigo (##Install driver for ROS From ROS Wiki page(http://wiki.ros.org/openni_kinect))<br>
  Openni<br>
  Kinnect camera<br>
  Pepper robot<br>

# 1.  Kinect driver for Ubuntu 14.04 and ROS indigo
sudo apt-get install ros-kinetic-openni-camera ros-kinetic-openni-launch<br>
sudo apt-get install git build-essential python libusb-1.0-0-dev freeglut3-dev openjdk-8-jdk<br>
sudo apt-get install doxygen graphviz mono-complete<br>

## Install OpenNI
cd ~/ mkdir kinect<br>
cd ~/kinect git clone https://github.com/OpenNI/OpenNI.git <br>
cd OpenNI git checkout Unstable-1.5.4.0 cd Platform/Linux/CreateRedist <br>
chmod +x RedistMaker <br>
./RedistMaker<br>

cd /yourpath/kinect/OpenNI/Platform/Linux/Redist/OpenNI-Bin-Dev-Linux-x64-v1.5.4.0 <br>
sudo ./install.sh<br>
cd ~/kinect git clone https://github.com/avin2/SensorKinect <br>
cd SensorKinect cd Platform/Linux/CreateRedist <br>
chmod +x RedistMaker <br>
./RedistMaker<br>

cd /yourpath/kinect/SensorKinect/Platform/Linux/Redist/Sensor-Bin-Linux-x64-v5.1.2.1 <br>
chmod +x install.sh <br>
sudo ./install.sh<br>

## Install Ros indigo OpenNI
sudo apt-get install ros-indigo-openni*<br>

## Install NITE

cd ~/kinect git clone https://github.com/arnaud-ramey/NITE-Bin-Dev-Linux-v1.5.2.23 <br>
cd /yourpath/kinect/NITE-Bin-Dev-Linux-v1.5.2.23/x64 <br>
sudo ./install.sh<br>

## Install openni_tracker
cd ~/catkin_ws/src <br>
git clone https://github.com/ros-drivers/openni_tracker.git<br>

## Remake Catkin Workspace
cd ~/catkin_ws <br>
catkin_make <br>
catkin_make install<br>

## launch openni and openni_tracker
roscore<br>
roslaunch openni_launch openni.launch<br>
rosrun image_view image_view image:=/camera/rgb/image_color<br>
rosrun image_view disparity_view image:=/camera/depth_registered/disparity<br>

cd ~/catkin_ws/devel <br>
source setup.bash <br>
rosrun openni_tracker openni_tracker<br>

## create package

roscreate-pkg kinect_pj rospy tf<br>
cd ~/yourpath/catkin_ws/src/kinect_pj/src <br>
chmod +x kinect_pj<br>

## launch kinect_pj

cd ~/catkin_ws/devel <br>
source setup.bash <br>
rosrun kinect_pj kinect_pj<br>

# 2.  Run the teleoperation command
kinect_pj(simulation)
kinect_pj(copyand)
Rename these files into kinect_pj under the kinect_pj/src folder. Change the permission to executable by use chmod 777 filename<br>

open multiple terminal to run the commands below:<br>
roscore<br>
roslaunch openni_launch openni.launch<br>
rosrun openni_tracker openni_tracker<br>
#check the ip and port in choreograph tool for the virtual machine<br>
rosrun kinect_pj kinect_pj --ip <ip> --port <port><br>


Reference:<br>
https://github.com/ros-drivers/openni_tracker/issues/9<br>
https://github.com/cltl/pepper/wiki/Installation<br>
https://github.com/ketchart/Pepper-Robot-controlled-by-Kinect-in-Ubuntu<br>


