This program executes Libviso, DLoop and g2o in parallel threads for trajectory estimation and optimization using stereo vision.

Procedure -

Install

a. Libviso2 - http://www.cvlibs.net/software/libviso/

b. DLoop - https://github.com/dorian3d/DLoopDetector (along with DLib and DBow2)

c. g2o - https://github.com/RainerKuemmerle/g2o

cd cair_online/

mkdir build
cd build
cmake ..
make -j5
./main
<-------------------------------->

Source code - main.cpp

Supporting files - src/*.cpp

Header files - includes/*.h

<-------------------------------->

Main function calls -

Libviso2 for intial trajectory estimates from src/helper.cpp - my_libviso2

DLoop Detector for loop closure from includes/demoDetector.h - run

g2o is called after every 500th frame and once at the end of trajectory.

<-------------------------------->

Parameters -

In main function

IMG_DIR1 - Directory where Images are stored. Format -> dir/loop1/left and dir/loop1/right

VOC_FILE - Vocabulary file. Generated from DBOW2

IMAGE_W, IMAGE_H - Image Width, Image Height - Keep default.

In helperfunctions.cpp

param.calib.f - focal length in pixels param.calib.cu - principal point (u-coordinate) in pixels param.calib.cv - principal point (v-coordinate) in pixels param.base - baseline in meters
In demoDetector.h

params.use_nss - use normalized similarity score instead of raw score params.alpha - nss threshold params.k - a loop must be consistent with 1 previous matches params.geom_check - use direct index for geometrical checking params.di_levels - use two direct index levels
In TemplatedLoopDetector.h

dislocal = number * f - for skipping 'number' of frames between loops.
