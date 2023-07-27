# Install Python 3.8
1. Install python 3.8
   ```
   sudo apt-get install python3.8 python3.8-dev python3.8-distutils python3.8-venv
   ```
2. Change it as the default version:
   ```
   sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 1
   ```
3. Install pip3:
   ```
   sudo apt-get -y install python3-pip
   ```
# Install ros
Follow guide: http://wiki.ros.org/noetic/Installation/Ubuntu

# Create a catkin workspace


# respeaker-ros
1. Not listed prerequisites:
   - pip:
   ```
   sudo pip install testresources pixel-ring speechrecognition
   ```
   - system-wide
   ```
   sudo apt-get install python3-pyaudio
   ```
   - ros pkgs:
   ```
   sudo apt-get install ros-noetic-sound-play ros-$ROS_DISTRO-speech-recognition-msgs ros-$ROS_DISTRO-catkin-virtualenv
   ```
2a. Build from **source**: https://index.ros.org/p/respeaker_ros/

   If you have trouble because of the `catkin_virtualenv`, make the `respeaker_ros` package dependent (compile it as the last package) to the other packages modifying the `CMakeLists.txt` and the `package.xml`
   
2b. If installed the package using apt-get and there are problems try: change the paths in the 2 files in `/home/ppm/catkin_ws/devel/lib/respeaker_ros` (named `speech_to_text.py` and `respeaker_node.py`)to point the python executable and the correct files under `/src`)
# intel realsense-ros
```
sudo apt-get install ros-$ROS_DISTRO-realsense2-camera
```
```
source devel/setup.bash
```
# Intel Realsense SDK
**DISCONNECT the camera**
Guide installation of intelrealsense in Jetson Orin Nano Developer kit. 
For Pyhton 3.8

```
sudo apt-get update && sudo apt-get -y upgrade
```
```
sudo apt-get install -y --no-install-recommends \
    python3 \
    python3-setuptools \
    python3-pip \
    python3-dev
```
```
sudo apt-get install -y git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev
```
```
sudo apt-get install -y libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
```
```
sudo apt-get install libusb-1.0-0-dev
```
```
sudo apt-get install python3.9-dev
```
```
git clone https://github.com/IntelRealSense/librealsense.git
```
```
cd librealsense/
mkdir build && cd build
cmake ../ -DFORCE_RSUSB_BACKEND=false -DBUILD_PYTHON_BINDINGS=true -DPYTHON_EXECUTABLE=/usr/bin/python3.8 -DCMAKE_BUILD_TYPE=release -DBUILD_EXAMPLES=true -DBUILD_GRAPHICAL_EXAMPLES=true -DBUILD_WITH_CUDA:bool=true
```
```
sudo make uninstall && make clean && make && sudo make install
```

Import pyrealsense2 using:
```
import pyrealsense2.pyrealsense2 as rs
```
# Install OpenPose
1. Install prerequisites:
```
sudo apt install libcanberra-gtk-module libcanberra-gtk3-module
```
And: https://cmu-perceptual-computing-lab.github.io/openpose/web/html/doc/md_doc_installation_1_prerequisites.html

2. Then follow the guide: https://cmu-perceptual-computing-lab.github.io/openpose/web/html/doc/md_doc_installation_0_index.html
3. Install systme-wide (needed to use OpenPose API outside its own folder):
```
sudo make install
```
To uninstall simply run in the `/build` foder:
```
sudo make uninstall
```

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
pip3 install tensorflow==2.12.0 # +nv23.01
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
