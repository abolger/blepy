blepy
=====

Python bindings for Bluegiga BLED112 Bluetooth Low Energy USB Dongle.

This project generates python api bindings for the Bluegiga BLED112 by parsing
the bleapi XML specification file. The user is required to have the Bluegiga
Bluetooth Smart SDK (available from http://techforum.bluegiga.com/BLED112). 
This project is in no way associated with Bluegiga.


Caveats
-------

This is a work in progress and probably won't "just work". It has been tested 
so far on Mac OS X and Raspberry Pi. Sending variable length messages is currently not implemented properly.


Api Generation
--------------

#. Install python prerequisites; numpy and ctypes (possibly already available
   on your system)

#. Run ``api_gen.py <XML file>`` where <XML file> is the file "bleapi.xml" found
   in the "api" folder of the Bluegiga SDK. This will generate "ble.py"
   
#. Compile the uart module (which is imported into "ble.py" by ctypes). This
   requires the "uart.c" and "uart.h" files from SDK/src/thermometer-demo
   ``gcc -o uart.so uart.c -shared``

Api Generation: WINDOWS ONLY
--------------
#. Follow steps 1 and 2 above for Python prerequisites.   

#. If you're on Windows and you don't have the GCC for windows yet, you can get the latest minimal distribution from here: http://sourceforge.net/projects/mingw/files/latest/download?source=files)

#. Add the line "#def PLATFORM_WIN 1" to your BlueGiga SDK's "uart.c" so that you get the Windows .so compiled object instead of the . 

#. Run the following:
    ``C:\MinGW\bin>gcc.exe -o uart.so C:\Bluegiga\ble-1.3.1-119\src\thermometer-demo\uart.c -DPLATFORM_WIN -shared -lsetupapi``
    ``C:\MinGW\bin>move uart.so C:\Your_BLEPY_DIRECTORIES\uart.so
    
#. Copy the "uart.so" file to the same location as "ble.py" 

#. Example Windows usage (assuming a BLE113 or BLUE112 USB dongle is plugged in and recognized as a comport:
    ``python demo.py COM75 scan``

Usage
-----
 
Take a look at "demo.py" to get an idea of how to use the library






