# Vireo Support For EV3
This library serves as a bridge between the [extended version of the LEGO EV3 firmware][1] and [Vireo][2] a compact runtime for executing LabVIEW Virtual Instruments.  It consists of additional Vireo primitives for EV3 functionality and Vireo entry points for use by the firmware.

#### Additional Vireo primitives
The files `EV3_Com.cpp`, `EV3_File.cpp`, `EV3_Input.cpp`, `EV3_Output.cpp`, `EV3_Sound.cpp`, and `EV3_UI.cpp` define Vireo primitives for controlling motors, reading sensors, drawing to the display, etc.  These primitives correspond roughly to operations in the EV3 firmware, and a large portion of this code is directly copied or derived from the EV3 firmware source.

#### Vireo Entry Points
The file `EV3_Entry.cpp` contains functions that enable the firmware to interact with Vireo.  These include functions for loading Vireo as a 3rd party VM and executing a Vireo program, among others.

## Build
 0. Get a (virtual) install of Linux.  We've used Ubuntu 12.04 virtualized with VMware, but other combinations should work.
 0. Get [Code Sourcery Lite for ARM version 2009q1-203][3], extract it, and add the path to CodeSourcery/Sourcery_G++_Lite/bin to your PATH environment variable.
 0. Get the [LEGO MINDSTORMS EV3 source code - Extended version][1] and specify its location by setting the EV3SOURCES_BASE variable in the [`Makefile`][4]
 0. Get the [VireoSDK][2] source code and specify its location by setting the VIREO_BASE variable in the [`Makefile`][4].
 0. Navigate to the [`build`][5] directory and run `make`.  This process gets the VireoSDK to build the libvireo.so library, compiles source files (which depend on headers from the EV3 source and Vireo), and links into the libvireobridge.so library (which depends on libvireo.so).  If it succeeded, you should find up-to-date libvireo.so and libvireobridge.so libraries in the [`build`][5] directory.

## Deploy
Copy the libvireo.so and libvireobridge.so libraries to the directory /home/root/lms2012/3rdparty-vm/ on an EV3 running the extended version of the firmware.  This can be done in LabVIEW with the module for LEGO MINDSTORMS using the "Load File on to Brick" block.  You may have to restart the EV3 if a 3rd party VM is already loaded.

[1]: https://github.com/mindboards/ev3sources-xtended
[2]: https://github.com/ni/VireoSDK
[3]: https://sourcery.mentor.com/GNUToolchain/release858
[4]: https://github.com/ni/VireoSupportForEV3/build/Makefile
[5]: https://github.com/ni/VireoSupportForEV3/build/

