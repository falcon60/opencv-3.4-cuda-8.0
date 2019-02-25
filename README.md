# Install Opencv 3.4 with CUDA 8.0 support on Ubuntu 16.04

## Install CUDA 8.0

Select the below options and download the installer

![CUDA 8.0 Installer](https://github.com/falcon60/opencv-3.4-cuda-8.0/blob/master/cuda_options.png)

Run the installer:
```bash
sudo dpkg -i /path/to/installer/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
```

Check for `cuda-8.0` folder in `/usr/local/`

## Check CUDA version:

```bash
cat /usr/local/cuda/version.txt
```
## Install Anaconda Python 3

https://www.anaconda.com/distribution/#download-section

## Create Conda Environment

```bash
conda create -n opencv_cuda python=3.6 numpy cmake
conda activate opencv_cuda
```

## Update and install the required repositories:

```bash
sudo apt-get -y update
sudo apt-get -y install git wget unzip build-essential pkg-config 
sudo apt-get -y install libatlas-base-dev gfortran libjasper-dev libgtk2.0-dev libavcodec-dev libavformat-dev
sudo apt-get -y install libswscale-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libv4l-dev
```
## Download OpenCV 3.4.2 

```bash
OPENCV_VERSION=3.4.2
wget https://github.com/opencv/opencv/archive/$OPENCV_VERSION.zip -O opencv3.zip
unzip -q opencv3.zip
mv /opencv-$OPENCV_VERSION /opencv
rm opencv3.zip
wget https://github.com/opencv/opencv_contrib/archive/$OPENCV_VERSION.zip -O opencv_contrib3.zip
unzip -q opencv_contrib3.zip
mv /opencv_contrib-$OPENCV_VERSION /opencv_contrib
rm opencv_contrib3.zip
```
## Create Build directory

```bash
mkdir /opencv/build
cd /opencv/build
```


## Use following CMAKE options

```bash
cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D BUILD_PYTHON_SUPPORT=ON \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D OPENCV_EXTRA_MODULES_PATH="~/opencv_contrib/modules" \
      -D BUILD_EXAMPLES=OFF \
      -D PYTHON_DEFAULT_EXECUTABLE=/home/madtitan/anaconda3/envs/opencv_cuda/bin/python3 \
      -D PYTHON3_INCLUDE_PATH=/home/madtitan/anaconda3/envs/opencv_cuda/include/python3.6m \
	    -D PYTHON3_LIBRARIES=/home/madtitan/anaconda3/envs/opencv_cuda/lib/python3.6/site-packages \
      -D BUILD_opencv_python3=ON \
      -D BUILD_opencv_python2=OFF \
	    -D ENABLE_PRECOMPILED_HEADERS=OFF\
      -D WITH_IPP=OFF \
      -D WITH_FFMPEG=ON \
      -D WITH_CUDA=ON \
      -D CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-8.0 \
      -D WITH_CUBLAS=ON \
      -D WITH_V4L=ON ..
```
Change the Anaconda Environment path according to your system

```bash
make -j$(nproc)
sudo make install
sudo ldconfig
```
