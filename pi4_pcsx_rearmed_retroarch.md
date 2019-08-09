# Compiling RetroArch PCSXReARMed for Pi4
## Prerequisites
	sudo apt install build-essential libx11-dev	libpng-dev

If not working try these: `sudo apt install build-essential libasound2-dev libudev-dev libxkbcommon-dev zlib1g-dev libfreetype6-dev libegl1-mesa-dev libgles2-mesa-dev libgbm-dev libavcodec-dev libsdl2-dev libsdl-image1.2-dev libxml2-dev yasm libavformat-dev libavdevice-dev libswresample-dev libavresample-dev libswscale-dev libv4l-dev libgl*-mesa-dev`
## Prepare files
- clone or download source from this repository: https://github.com/libretro/pcsx_rearmed.git
- unzip and open console in the directory
- open file Makefile.libretro and change the part with `#Raspberry Pi 4`
- replace `CFLAGS += -marm -mcpu=cortex-a72 -mfpu=neon-fp-armv8 -mfloat-abi=hard` with `CFLAGS += -marm -mcpu=cortex-a72 -mfloat-abi=hard`
- replace `ASFLAGS += -mcpu=cortex-a72 -mfpu=neon-fp-armv8 -mfloat-abi=hard` with `ASFLAGS += -mcpu=cortex-a72 -mfloat-abi=hard`

## Compilation
	make -f Makefile.libretro platform=rpi4 ARCH=arm USE_DYNAREC=1 HAVE_NEON=0 BUILTIN_GPU=peops

## Wrapping this up
- you should see file `pcsx_rearmed_libretro.so`
- copy it to your RetroArch cores directory (probably this one): `~/.config/retroarch/cores`
