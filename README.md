Fwknop-gui is intended to be a cross platform graphical client for sending SPA knocks to fwknopd. 
It is based on the interface of Fwknop2 on Android.

Binary downloads for Windows and Mac are hosted at http://incomsystems.biz/fwknop-gui

Building from source is generally done by creating a build folder in the source directory, and running "cmake .." in that build folder. Then run make and sudo make install.

To build on Windows, use the msys2 project from http://msys2.github.io/
Once installed, don't launch the msys2 shell. Instead, use the "MinGW-w64 Win32 Shell" Start by running "update-core", installing those updates, and then closing that shell and reopening it.

From there, run:
pacman -S mingw-w64-i686-toolchain
pacman -S make mingw-w64-i686-make mingw-w64-i686-libtool texinfo autoconf automake tar

Download the latest tarball from http://www.cipherdyne.org/fwknop/download/ and use tar -xf fwknop-2.* to unpack.  Then run:

./configure --disable-server --disable-client --disable-stack-protector
mingw32-make

This should just work as of Fwknop 2.6.9.

For qrcode support, download the latest realease from https://fukuchi.org/works/qrencode/
./configure, build, and build install

Next, unpack the fwknop-gui source, and create a build directory.  Run cmake .. -G"MSYS Makefiles" twice! and then make to build.


On Mac, I've had to compile both wxWidgets and libqrencode from source.
Macports or Homebrew should suffice to install a usable toolchain to bootstrap compiling.

