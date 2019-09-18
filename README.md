OpenDTAM for Opencv 4.1
========

An open source implementation of DTAM

Based on Newcombe, Richard A., Steven J. Lovegrove, and Andrew J. Davison's "DTAM: Dense tracking and mapping in real-time."

## Build Instructions on Ubuntu 18.04

Tested in this environment

* Ubuntu 18.04 x64
* GCC 7.4 for C++
* GCC 6.5 for CUDA
* Boost 1.65
* OpenCV 4.1.1
* Cuda Toolkit 9.1
* GTX-970m sm-52

### Install dependencies From Ubuntu 18.04 repository

#### qtbase5-dev

#### libboost-dev

#### libgstreamer1.0-dev

#### Cuda

Version 9.1 was used, from the Ubuntu nvidia-driver-390.deb and associated nvidia-compute-utils-390 etc.


#### OpenCV 4, OpenCV_Contrib (CudaImgProc module is required), and opencv_extra (data for unit tests)

git clone https://github.com/opencv/opencv.git

git clone https://github.com/opencv/opencv_contrib.git

git clone https://github.com/opencv/opencv_extra.git

```
cd opencv 
git checkout tags/4.1.1 
mkdir build 
cd build 
cmake_gui ../ 
```

You will need to provide the path to opencv_contrib and to opencv_extra/testdata .

You will need to specify WITH CUDA and CUFFT 

Set the CUDA_ARCH_BIN to the 'compute capability' of you Nvidia GPU. '52' for GTX-9xx series GPUs.

Set the CUDA_HOST_COMPILER to one that is compatible with your version of CUDA. 'gcc-6' or lower for CUDA 9.1 .

See the OpenCV-4-CMakeCache.txt in this directory for the full parameters as tested. 

```
make -j8 
```(set to your number of CPU cores)


#### Run the unit tests

```
make check 
```(to run unit tests), 

especially run 

```
build/bin/opencv_test_videoio 
``` 

and 

```
build/bin/opencv_test_cudaimgproc 
``` .

If these tests fail, you will probably have to add specific libraries _and_ their headers (packages ending in '-dev.deb' ) .

If you are using a Debian or Ubuntu dervived Linux distro, it is recommended to use Synaptic Package Manager to find and install packages.


#### Install OpenCV-4

When the tests work, 

```
sudo make install 
```


### Build OpenDTAM

```
cd OpenDTAM
mkdir build
cd build
cmake_gui ../Cpp

Set the CUDA_ARCH_BIN to the 'compute capability' of you Nvidia GPU. '52' for GTX-9xx series GPUs.

Set the CUDA_HOST_COMPILER to one that is compatible with your version of CUDA. 'gcc-6' or lower for CUDA 9.1 .

make -j8
````

### Run OpenDTAM
For the following command, replace `$TRAJECTORY_30_SECONDS` with the path to the directory of the same name.
```bash
./a.out $TRAJECTORY_30_SECONDS
```
Assuming you are executing this command from the build folder, as shown above, enter the following:
```bash
./a.out ../Trajectory_30_seconds
```
