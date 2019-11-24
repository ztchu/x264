Reference：[Windows下编译ffmpeg，链接libx264静态库](https://blog.csdn.net/u013295518/article/details/90273899)


Compilation steps:

(1) Install msys2:
http://repo.msys2.org/distrib/x86_64/

(2) Install mingw
Start msys2, and execute:
pacman -Syuu

then:
pacman -S --needed mingw-w64-x86_64-toolchain
pacman -S --needed mingw-w64-i686-toolchain
pacman -S --needed base-devel
pacman -S vim

optional:
pacman -S nasm


then:
Add "C:/msys64/mingw64/bin" to environment path.

then:
Execute "gcc -v" to check if the installation is successful.


(3) configure
configuration options may cause compile failed.
This is the configuration options by trying:

compile static library: --enable-static
compile shared library: --enable-shared

compile 32-bit library: --host=i686-w64-mingw32
compile 64-bit library: --host=x86_64-w64-mingw32

WARN:
Please start mingw32.exe if you want to build x264 with "--host=i686-w64-mingw32";
start mingw64.exe if you want to build x264 with "--host=x86_64-w64-mingw32";

Disable asm:
 --disable-asm

../configure --enable-shared --enable-pic --prefix=./x264_install --host=i686-w64-mingw32 --disable-cli

(4) make
make

make install

(5) export
If you need shared library, maybe you should export lib file on windows:
Use Visual studio '  developer command prompt to export:
LIB /DEF:libx264.def /MACHINE:x86

If the export library is libx264.dll.a, change it as libx264.dll.lib directly.