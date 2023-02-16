# MVSNet depthfusion配置流程
## 原文内容
R/MVSNet itself only produces per-view depth maps. To generate the 3D point cloud, we need to apply depth map filter/fusion for post-processing. As our implementation of this part is depended on the Altizure internal library, currently we could not provide the corresponding code.  
Fortunately, depth map filter/fusion is a general step in MVS reconstruction, and there are similar implementations in other open-source MVS algorithms. We provide the script depthfusion.py to utilize fusibile for post-processing (thank Silvano Galliani for the excellent code!).

To run the post-processing:

- Check out the modified version fusibile git clone https://github.com/YoYo000/fusibile
- Install fusibile by cmake . and make, which will generate the executable at FUSIBILE_EXE_PATH
- Run post-processing (--prob_threshold 0.8 if using 3DCNNs): python depthfusion.py --dense_folder TEST_DATA_FOLDER --fusibile_exe_path FUSIBILE_EXE_PATH --prob_threshold 0.3
- The final point cloud is stored in TEST_DATA_FOLDER/points_mvsnet/consistencyCheck-TIME/final3d_model.ply.


使用Origin Fusible代码融合出来的点云颜色是没有的，这里YaoYao通过修改了代码使得Gipuma融合出来的点云是由颜色的, 下面是YaoYao给出的代码: [click here](https://github.com/YoYo000/fusibile)
## CMakeList配置需求
```
cmake_minimum_required (VERSION 3.9)
project (fusibile)

# Enable C++11 globally
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Support IDEs: https://cliutils.gitlab.io/modern-cmake/chapters/features/ides.html
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER "cmake-default-targets")

find_package(OpenCV REQUIRED )
find_package(CUDA 6.0 REQUIRED ) # For Cuda Managed Memory and c++11

if(NOT DEFINED CMAKE_CUDA_STANDARD)
    set(CMAKE_CUDA_STANDARD 11)
    set(CMAKE_CUDA_STANDARD_REQUIRED ON)
endif()

include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(.)

# from https://en.wikipedia.org/wiki/CUDA#GPUs_supported
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 --use_fast_math --ptxas-options=-v --compiler-options -Wall -gencode arch=compute_30,code=sm_30 -gencode arch=compute_32,code=sm_32 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_53,code=sm_53 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_62,code=sm_62 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_72,code=sm_72 -gencode arch=compute_75,code=sm_75)
#set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 --use_fast_math --ptxas-options=-v -std=c++11 --compiler-options -Wall -gencode arch=compute_52,code=sm_52)

if(CMAKE_COMPILER_IS_GNUCXX)
    add_definitions(-std=c++11)
    add_definitions(-Wall)
    add_definitions(-Wextra)
    add_definitions(-pedantic)
    add_definitions(-Wno-unused-function)
    set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3 -ffast-math -march=native") # extend release-profile with fast-math
    #add_definitions(-march=native)
endif()


# for YouCompleteMe
set( CMAKE_EXPORT_COMPILE_COMMANDS 1 )

# For compilation ...
# Specify target & source files to compile it from
cuda_add_executable(
    fusibile
    cameraGeometryUtils.h
    vector_operations.h
    camera.h
    globalstate.h
    algorithmparameters.h
    cameraparameters.h
    linestate.h
    displayUtils.h
    mathUtils.h
    fileIoUtils.h
    fusibile.cu
    main.cpp
    )
# https://cliutils.gitlab.io/modern-cmake/chapters/packages/OpenMP.html
find_package(OpenMP)

# For linking ...
# Specify target & libraries to link it with
target_link_libraries(fusibile
	${OpenCV_LIBS}
	OpenMP::OpenMP_CXX
	)


include(FeatureSummary)
feature_summary(WHAT ALL)

```

### 针对CMakeList.txt文件修改
官方文件由于是14年的文件，那时候还不支持2080ti等算力的显卡。我通过``` cmake . ```和``` make ```编译得到的fusibile程序，运行报```no kernel image is available for execution on the device```的错误，因此为了兼容我的显卡以及多种其他算力不同cuda版本的显卡，我修改了CMAKELIST.txt文件。

将下面内容注释掉:
```
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 --use_fast_math --ptxas-options=-v -std=c++11 --compiler-options -Wall -gencode arch=compute_52,code=sm_52)
```
替换为了如下内容:
```
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 --use_fast_math --ptxas-options=-v --compiler-options -Wall -gencode arch=compute_30,code=sm_30 -gencode arch=compute_32,code=sm_32 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_53,code=sm_53 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_62,code=sm_62 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_72,code=sm_72 -gencode arch=compute_75,code=sm_75)
```

目前好像还不支持3090等30系显卡，但是20系显卡都支持了，后续的需要进行修改就好了.

## 具体配置
- 将https://github.com/YoYo000/fusibile的代码clone下来
- 前提是配置好下面所需要的配置：CMAKE、OPenCV和CUDA
- 通过cmake.和make来安装fusible
  - 进入fusible文件夹
  - 输入``` cmake .```, 得到如下数据
```
-- The following OPTIONAL packages have been found:

 * OpenMP

-- The following REQUIRED packages have been found:

 * OpenCV
 * Threads
 * CUDA (required version >= 6.0)

-- Configuring done
-- Generating done
-- Build files have been written to: /file/sync_files/FasterMVSNet/fusible
```
  - 输入make, 编译完成之后文件夹会出现一个fusible文件没有后缀，表示成功了。
  - 如果需要的话，需要使用如下命令来清除缓存
```
rm -rf CMakeCache.txt
```

## Linux安装CMAKE
1. 通过如下命令查看Linux位数
```
getconf LONG_BIT
```
2. 获取cmake源码包，先创了一个文件夹来存储cmake, 根据官方配置需求文件，得到我们需要一个CMAKE版本大于3.9
```
mkdir app

cd app
```
然后要去CMAKE[官网](https://cmake.org/download/)去获取对应的CMAKE链接, 使用如下命令下载:
```
wget install https://github.com/Kitware/CMake/releases/download/v3.21.2/cmake-3.21.2.tar.gz
```
这里我下载的是3.21版本的CMAKE.

3. 解压源码
```
tar xzvf cmake-3.21.2.tar.gz
```

4. 安装gcc(Ubuntu使用apt-get安装，Linux使用yum安装)
```
# Ubuntu
apt-get install gcc

# Linux
yum install gcc-c++
```

5. 安装cmake，先进入解压后的cmake的目录
```
cd cmake-3.21.2

./bootstrap
```
如果编译出现如下信息:
```
 Could NOT find OpenSSL
```
Ubuntu系统可以执行如下命令安装相关依赖:
```
apt-get update
apt-get install libssl-dev
```
安装完成之后再重新编译就好了。

6. 在当前目录执行如下命令安装make
```
make install
```
7. 完成之后使用如下命令查看cmake版本
```
cmake --version
```

## Linux安装OpenCV
1. 按照之前的步骤安装完cmake
2. 安装依赖环境
```
apt-get install build-essential libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev

apt-get install libgtk2.0-dev

apt-get install pkg-config
```
3. 去OpenCV[官网](https://opencv.org/releases/)下载源码，这里我是将源码下载下来，然后在上传到服务器上的，可以使用wget来进行源码的下载，命令如下:
```
wget install https://github.com/opencv/opencv/archive/4.5.3.zip
```

4. 解压完文件
```
unzip -n opencv-4.5.3.zip
```

5. 解压完文件之后，进入目录，创建build目录
```
cd opencv-4.5.3

mkdir build
```
6. 使用如下命令清除CMakeCache缓存
```
rm -rf CMakeCache.txt
```
这个方法是进入到build文件夹之后，使用cmake出现如下错误时使用:
```
CMake Error: The source directory "/file/app/opencv-4.5.3/build" does not appear to contain CMakeLists.txt.
```

7. 进入build文件夹，使用cmake命令
```
cmake -D CMAKE_BUILD_TYPE=Release -D CMAKE_INSTALL_PREFIX=/usr/local ..
```
如果安装了Anaconda建议使用如下命令:
```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_SHARED_LIBS=OFF -D WITH_OPENMP=ON -D ENABLE_PRECOMPILED_HEADERS=OFF ..

```
切记不能在cmake配置下面的环境变量，否则会报错！！！
类似下面这种
```
  Some of these libraries may not be found correctly. Call Stack (most recent call first):   cmake/OpenCVModule.cmake:1273 (ocv_add_executable)   modules/highgui/CMakeLists.txt:272 (ocv_add_accuracy_tests)
```
8. 执行结束之后，在使用make进行编译
```
make -j8
```

9. 使用如下命令进行安装
```
make install
```
10. 配置环境，使用vim打开/etc/ld.so.conf，在最后一行加上/usr/local/lib
```
vim /etc/ld.so.conf

include /usr/local/lib
```

然后运行如下命令生效:
```
ldconfig
```

11. 修改bash.bashrc文件
```
vim /etc/bash.bashrc
```
在文件末尾添加上如下内容:
```
PKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig
export PKG_CONFIG_PATH
```
然后在命令输入如下命令生效:
```
source /etc/bash.bashrc
```

12. 检查是否生效
```
cd /usr/local/lib
ls
```

![figure.1](http://image-storage-zs.test.upcdn.net/stu0IU.png)

## 问题
### 报错GL/gl.h: No such file or directory
使用如下命令安装:
```
sudo apt-get install mesa-common-dev
sudo apt-get install libgl1-mesa-dev libglu1-mesa-dev
```