# TeleSculptor from Kitware

TeleSculptor is a cross-platform desktop application for photogrammetry. It was designed with a focus on aerial video, such as video collected from UAVs, and handles geospatial coordinates and can make use of metadata, if available, from GPS and IMU sensors. However, the software can also work with non-geospatial data and with collections of images instead of metadata. TeleSculptor uses Structure-from-Motion techniques to estimate camera parameters as well as a sparse set of 3D landmarks. It uses Multiview Stereo techniques to estimate dense depth maps on key frame and then fuses those depth maps into a consistent surface mesh which can be colored from the source imagery.

TeleSculptor provides a graphical user interface with Qt, 3D visualization with VTK, and photogrammetry algorithms with KWIVER. This project was previously called MAP-Tk (Motion-imagery Aerial Photogrammetry Toolkit). The MAP-Tk name is still scattered throughout the source code. MAP-Tk started as an open source C++ collection of libraries and tools for making measurements from aerial video. The TeleSculptor application was added to the project later. The original software framework and algorithm were then refactored into KWIVER and then expanded to address broader computer vision problems. While KWIVER is now a more broad set of tools, TeleSculptor remains an application focused on photogrammetry.

The advantage of the KWIVER software architecture (previously MAP-Tk) is that it is highly modular and provides an algorithm abstraction layer that allows seamless interchange and run-time selection of algorithms from various other open source projects like OpenCV, VXL, Ceres Solver, and PROJ4. The core KWIVER library (vital) and tools are light-weight with minimal dependencies (C++ standard library, and Eigen). TeleSculptor is written to depend only on the KWIVER "vital" library. Additional capabilities are provided by KWIVER arrows (plugin modules) that use third party libraries to implement various abstract algorithm interfaces defined in the KWIVER vital library. This means that new plugins can be dropped into TeleSculptor to enable alternative or new functionality by adjusting some settings in a configuration file. While TeleSculptor provides a default workflow that works out of the box, it is not just an end user tool. It is designed to be highly configurable to support research into to algorithms and new problem domains.

https://github.com/Kitware/TeleSculptor

## To Build and Run

### Build

Install dependencies
```bash
$ sudo apt-get install build-essential libgl1-mesa-dev libxt-dev
$ sudo apt-get install libexpat1-dev libgtk2.0-dev liblapack-dev
```

Clone source code and prepare for build
```bash
$ mkdir telesculptor
$ 
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE:STRING=Release ../src
```

Alternatively ccmake can be used for cmake options
`$ ccmake ../src`
Don't enable CUDA because it will also try to build nvidia decoder acceleration which is deprecated since CUDA10

Make
`$ make`

If you got error for finding `open()` and `O_RDWR`, add these includes to 
`telesculptor/build/external/fletch-build/build/src/VXL/contrib/oul/oufgl/frame_grabber_v4l.cxx`
```cpp
#include <fcntl.h>    /* For O_RDWR */
#include <unistd.h>   /* For open(), creat() */
```

If you got error for downloading eigen, you can download it manually and copy into expected folder
```bash
$ wget http://ftp.mi.fu-berlin.de/pub/OpenMS/contrib-sources/eigen-3.3.4.tar.gz
$ cp eigen-3.3.4.tar.gz telesculptor/build/external/fletch/Downloads/eigen-3.3.4.tar.gz
```


### Run


## Results and Screenshots;
