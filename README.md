# Install Opencv 3.4 with CUDA 8.0 support on Ubuntu 16.04

## Install CUDA 8.0

Select the below options and download the installer

![CUDA 8.0 Installer](https://github.com/falcon60/opencv-3.4-cuda-8.0/blob/master/cuda_options.png)

Check for `cuda-8.0` folder in `/usr/local/`

Check CUDA version by typing following command in terminal:

```bash
cat /usr/local/cuda/version.txt
```
Install Anaconda Python 3

https://www.anaconda.com/distribution/#download-section


Update and install the following repositories:

```bash
sudo apt-get -y update
sudo apt-get -y install python3 python3-dev git wget unzip cmake build-essential pkg-config 
sudo apt-get -y install libatlas-base-dev gfortran libjasper-dev libgtk2.0-dev libavcodec-dev libavformat-dev
sudo apt-get -y install libswscale-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libv4l-dev
```
