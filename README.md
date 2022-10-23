## Credits 
1) forked from `https://github.com/hominoids/sgminer-arm` 
2) for Android Port i got help from `https://github.com/Pyogenics` 
3) 
4)
5)
6)
#### I will mention credit when projects complete, project still under development.
#### I want help for kernel optimization for Adreno && ARM-Mali GPU 
#### In this project ALL kernel optimise for AMD 
 Contact Discord `HappY#3730`
# 
# Warning
# This Projects have no warranty, so everyone use your own risk

# how to build && install

building dependency ```pkg up && pkg upg && pkg i build-essential libtool cmake yasm make wget git libjansson libgmp opencl-headers libmicrohttpd libuv* clang binutils```

add OPENCL LIB PATH to .bashrc

```
nano ~/.bashrc

export LD_LIBRARY_PATH=$PREFIX/lib:/vendor/lib64:/vendor/lib64/egl
```

press `control+x` then type `y` exit from termux && re-open termux

now check opencl

```
git clone https://github.com/Oblomov/clinfo
cd clinfo
make
./clinfo.real

```


then install gcc because clang cannot compile `sgminer-android`

```

curl -LO https://its-pointless.github.io/setup-pointless-repo.sh

bash setup-pointless-repo.sh

pkg i gcc-10 libgccjit-10-dev libgomp-10 bthread

```

now you should install OpenCL driver for (Adreno && Arm-Mali)

```
Adreno

ln -s /system/vendor/lib64/libOpenCL.so $PREFIX/lib/libOpenCL.so

ARM-Mali

ln -s /system/vendor/lib64/egl/libmali.so $PREFIX/lib/libOpenCL.so
```
#### edit this line, after add save && exit
```
nano $PREFIX/include/bthread.h
```
#### add this line 
```
#include <pthread.h>
```

#### Example:

# compile the thing:

```
git clone https://github.com/Saikatsaha1996/sgminer-arm
cd sgminer-arm 
git submodule init 
git submodule update 
autoreconf -fi

CFLAGS="-O3 -Wall -march=armv8-a+simd+crypto+crc -mtune=cortex-a77 -std=gnu99 -fcommon" CPPFLAGS="-O3 -Wall -march=armv8-a+simd+crypto+crc -mtune=cortex-a77 -std=gnu99 -fcommon" LDFLAGS="-L$PREFIX/lib -lbthread -lpthread -lOpenCL -fcommon" ./configure --disable-adl --disable-adl-checks --disable-git-version 
```

now you can see in your screen `OPENCL FOUND && GPU MINING SUPPORT ENABLED`

now just run `make -j4`

now start mining `./sgminer -k <algo> -o <pool:port> -u <wallet_address> -p <password> -I d`

for more info `./sgminer --help`
