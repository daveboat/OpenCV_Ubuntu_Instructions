Some instructions (mostly so I can refer to what I did) for building opencv >=4 with CUDA support

## 1. Install dependencies
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libjpeg-dev libtiff-dev libpng-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libavutil-dev libavresample-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev
sudo apt-get install libopenblas-dev libatlas-base-dev gfortran
sudo apt-get install linux-image-generic linux-image-extra-virtual
sudo apt-get install linux-source linux-headers-generic
sudo apt-get install libhdf5-serial-dev
```
## 2. Clone OpenCV and OpenCV-contrib from github
```
git clone https://github.com/opencv/opencv.git
git clone https://github.com/opencv/opencv_contrib.git
```
## 3. Go into cloned opencv directory and create build folder
```
cd opencv
mkdir build && cd build
```
## 4. Run CMake (can take a few minutes, depending on your computer). NOTE: Replace /full/path/to/opencv_contrib/modules with your path to opencv_contrib/modules
```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_CUDA=ON -D CMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 -D INSTALL_PYTHON_EXAMPLES=ON -D OPENCV_EXTRA_MODULES_PATH=/full/path/to/opencv_contrib/modules -D BUILD_EXAMPLES=ON ..
```
(Optional) Check number of CPU cores available
```
nproc
```
## 5. Build and install opencv (this can take more than an hour, depending on your computer)
```
make -j$(nproc) # or replace $(nproc) with the number of cores you want to use
make install
sudo ldconfig
```