# InstallScriptDetectorn2onRaspi
required steps to install detectron2 on raspberry pi 3B+


# Step1: Install Raspian
1. download Raspberry Pi Imager from from https://www.raspberrypi.org/downloads/ for your operation system. I use windows version  (Raspberry Pi Imager for Windows) 
2. install Pi Imager and and select "Raspbery Pi OS (32 bit) as operating system within Imager OS Selection window. 
3. insert the SD Card into your Raspberry Pi 3B+ and turn it on
4. after booting the Raspber Pi OS, open the virtual terminal using Alt+Ctrl+T and give following commands:
$ sudo apt-get install update
$ sudo apt-get install upgrade
5. after finishing the updates, reboot your Raspberry with the follwoing command: 
$ sudo reboot 

#Step2: install OpenCv 4.2.0
1. first get sure that the version of python3 is >= 3.7

2. change you swap size : 
2.1. open your swap configuration file using :
$ sudo nano /etc/dphys-swapfile
2.2. witihng the dphys-swapfile change the "swapfile=100" to "swapfile=1024" and save and close it
2.3. affect the changes using: 
$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start





2. perform following commands

$ sudo apt-get purge wolfram-engine
$ sudo apt-get purge libreoffice*
$ sudo apt-get clean
$ sudo apt-get autoremove
$ sudo apt-get install build-essential cmake pkg-config
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
$ sudo apt-get install libgtk2.0-dev libgtk-3-dev
$ sudo apt-get install libatlas-base-dev gfortran
$ sudo apt-get install python2.7-dev python3-dev
$ cd ~

3. download opencv from opencv.org under : https://github.com/opencv/opencv/archive/4.2.0.zip
4. unzip it and change the folder name to "opencv"
5. download contribution of open cv from : https://github.com/opencv/opencv_contrib/archive/4.2.0.zip
6. unzip the file and change the folder to "opencv_contrib"
7. perform following commands:

$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python get-pip.py
$ pip install numpy

$ cd ~/opencv/
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE     -D CMAKE_INSTALL_PREFIX=/usr/local     -D INSTALL_PYTHON_EXAMPLES=ON     -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules     -D BUILD_EXAMPLES=ON ..
$ make -j4
$ sudo make install
$ sudo ldconfig
5. remove the installation files and folders (achte auf der dateinenamn, könnte hier falsch sein): 
$ cd ..
$ cd ..
$ rm -r -f opencv opencv_contrib opencv.4.2.0 opencv_contrib-4.2.0 
6. install following packages: 
$ sudo apt install libatlas-base-dev
$ sudo pip3 install h5py
$ sudo pip3 install -U setuptools

# step 5: Install Pytorch4.0.0
ATTENTION: this step does not work on raspberry pi3 b+. it crashes on 94%. therefore precompiled whil file are downloaded from "https://wintics-opensource.s3.eu-west-3.amazonaws.com/torch-1.4.0a0%2B7963631-cp37-cp37m-linux_armv7l.whl " and installed using pip3 install *.whl"
before testing it, you need maybe to install numpy using "pip3 install numpy" command in command line
furthemore, you need to install libatlas using apt. for this purpose  use the fllowing command 
$ sudo apt-get install libatlas-base-dev

in order to test the installation open python3 and give the "import torch" command. if you get some 
-------------------------------------------is not working -------------------------
(followed from this link :https://medium.com/hardware-interfacing/how-to-install-pytorch-v4-0-on-raspberry-pi-3b-odroids-and-other-arm-based-devices-91d62f2933c7) 
$ sudo apt install libopenblas-dev libblas-dev m4 cmake cython python3-dev python3-yaml python3-setuptools
$ mkdir pytorch_install && cd pytorch_install
$ git clone --recursive https://github.com/pytorch/pytorch
$ cd pytorch

and define environmental vraibales: 

$ export NO_CUDA=1
$ export NO_DISTRIBUTED=1
$ export NO_MKLDNN=1 
$ export NO_NNPACK=1
$ export NO_QNNPACK=1
--------------------------------------------------till here is not working----------------------------------
# Step optional Install tensorflow 
$ sudo pip3 uninstall tensorflow
$ sudo pip3 install tensorflow-1.8.0-cp35-none-linux_armv7l.whl
$ sudo pip3 uninstall mock
$ sudo pip3 install mock
$ sudo apt-get install libhdf5-dev
$ sudo pip3 install h5py
$ sudo pip3 install mtcnn




validate the installation: 
$ cd 
$ python3
>>> from __future__ import print_function
>>> import torch
>>> a = torch.rand(5,3)
>>> print (a)




pip3 install torch-utils
pip3 install -U torch torchvision
pip3 install git+https://github.com/facebookresearch/fvcore.git
git clone https://github.com/facebookresearch/detectron2 detectron2_repo
pip3 install -e detectron2_repo
