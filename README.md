# Install pyhont 3.8 and OpenPose
1. Install python 3.8
```
sudo apt-get install python3.8 python3.8-dev python3.8-distutils python3.8-venv
```
2. Install prerequisites: https://cmu-perceptual-computing-lab.github.io/openpose/web/html/doc/md_doc_installation_1_prerequisites.html
Then follow the guide: 
# Intel Realsense SDK
Guide installation of intelrealsense in Jetson Orin Nano Developer kit. 
For Pyhton 3.8

```
sudo apt-get update && sudo apt-get -y upgrade
sudo apt-get install -y --no-install-recommends \
    python3 \
    python3-setuptools \
    python3-pip \
    python3-dev

sudo apt-get install -y git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev

sudo apt-get install -y libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev

sudo apt-get install libusb-1.0-0-dev

sudo apt-get install python3.9-dev

git clone https://github.com/IntelRealSense/librealsense.git
cd librealsense/
mkdir build && cd build
cmake ../ -DFORCE_RSUSB_BACKEND=false -DBUILD_PYTHON_BINDINGS=true -DPYTHON_EXECUTABLE=/usr/bin/python3.8 -DCMAKE_BUILD_TYPE=release -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true -DBUILD_WITH_CUDA:bool=true
sudo make uninstall && make clean && make && sudo make install
```

Import pyrealsense2 using:
```
import pyrealsense2.pyrealsense2 as rs
```
# ROS
Follow guide: http://wiki.ros.org/noetic/Installation/Ubuntu
# respeaker-ros
1. Installation guide: https://index.ros.org/p/respeaker_ros/
```
sudo apt-get install ros-noetic-respeaker-ros
```
2. Change the paths in the 2 files in `/home/ppm/catkin_ws/devel/lib/respeaker_ros` (named `speech_to_text.py` and `respeaker_node.py`)to point the python executable and the correct files under `/src`
# tensorflow for Jetson
Create environment:
```
python -m venv $ENV_NAME
```
This will create a folder named $ENV_NAME. Source (activate) it:
```
source $ENV_NAME/bin/activate
```
Required packages here: https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html

and then install Tensorlow using:
```
sudo pip3 uninstall  tensorflow==2.12.0 # +nv23.01
```
If the installation succeeded but still importing tensorflow gives errors, use:
```
pip3 show tensorflow
```
to see the "Location" of the package and add it to the python path. It should be something like this:
```
export PYTHONPATH=/usr/local/lib/python3.8/dist-packages:$PYTHONPATH
```
To automatically execute this command, just append it to the `$env-name/bin/activate` file (as if it was the `.bashrc` file)
