This is a port of DOOM based on the original ID software source code release. It
is built for the MIPS CPU and then recompiled to 65816 code using my MIPS recompiler.

This port requires a C64/C128 with a SuperCPU v2 and 16MB RAM. PAL, NTSC (old and new)
as well as DREAN should be supported but it has only been tested on real PAL hardware.

While this DOOM port isn't meant to be taken seriously, it has proven quite
useful for testing and improving the MIPS recompiler as DOOM is a rather complex
and large application.

Some parts has been rewritten in 65816 assembler for better performance:

 * Fixed point multiply/divide
 * DrawColumn and DrawSpan
 * Chunky to bitmap conversion

DOOM is controlled using a joystick in port 2 and the keyboard. By default it will
run in a 4-color mode. It can be switched to a 16-color FLI color mode from the main
menu. The number in the upper left corner is the framerate.

NOTES:
  . The 16-color FLI mode is fullscreen on real hardware but VICE doesn't currently
    support the method used to create a fullscreen FLI display.
  . VICE has some issues with timing. Code to detect and work around those issues is
    included, but has only been tested on real PAL hardware and may fail on NTSC/DREAN.
  . Supporting the v1 SuperCPU could be possible, but would require dropping the double
    buffering.
  . Loading and saving game progress isn't supported.

The original DOOM1.WAD shareware WAD has been embedded in doom.reu and may be extracted if desired:

dd skip=4192588 count=4196020 if=wolf.reu of=DOOM1.WAD bs=1

Running in VICE:

xscpu64.exe -reu -reusize 16384 +reuimagerw -reuimage doom.reu -autostartprgmode 1 -autostart io.prg

Running on real hardware can be done using an FD-2000 or compatible diskdrive by
writing the D2M images to real floppy disks.

The loader is based on the "Covert Bitops Loadersystem V2.26" which supports a lot of
different hardware. I have experienced some issues while loading DOOM from floppies,
but if I copy it to the IDE64 using the IDE64 file manager, it does load and run fine
from there. (It also works fine using the d2m images in VICE.) If you try it on real
hardware, please let me know if you have any issues loading DOOM.

NOTE: The loader is quite flexible and will allow you to split files should you want to put
the files on different media. All you need to do is to split the files and name them like
the original but with the extension ".0", ".1", ... as I did with the DOOM1.WAD file. You
can also do the opposite and merge any split files if you decide to put them on some mass
storage device like the IDE64.

Contact:

Write to me (Mathias Roslund) at: maro [at] amidog [dot] se

History:

1.2 (2017-06-06): Uses much improved C64 code from the Wolf3D port which means a more complete
	and faster clib, double buffered display and a number of bugfixes. Optimized fixed divide.
1.1 (2014-11-03): Replaced the ugly half-width rendering hack with a proper implementation,
	which means that low detail mode now works. Added assembler versions of some blitting
	routines. Tweaked GCC options and upgraded to GCC 4.8.3 for a little more performance.
	Fixed map rendering. Added 16 color FLI mode, press P to toggle between	4 color and 16
	color mode.
1.0 (2014-09-29): First release.
