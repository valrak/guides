# Compiling RetroArch on Rpi4
## Prerequisites
	sudo apt install build-essential libasound2-dev libudev-dev libxkbcommon-dev zlib1g-dev libfreetype6-dev libegl1-mesa-dev libgles2-mesa-dev libgbm-dev libavcodec-dev libsdl2-dev libsdl-image1.2-dev libxml2-dev yasm libavformat-dev libavdevice-dev libswresample-dev libavresample-dev libswscale-dev libv4l-dev libgl*-mesa-dev

## Download RetroArch source
- https://github.com/libretro/RetroArch/releases (source code)
- untar/unzip to directory

## Compile
- in console, go to the directory with untar/unzipped RetroArch and run `CFLAGS='-mfpu=neon -mtune=cortex-a72 -march=armv8-a' ./configure --enable-alsa --enable-udev --enable-neon --disable-videocore --enable-opengles --enable-opengles3 --disable-opengl1 --enable-x11`
- `make`
- optionally: `sudo make install`

## Online updater
- run RetroArch and quit it.
- edit `~/.config/retroarch/retroarch.cfg`
- set `core_updater_buildbot_url` to `http://buildbot.libretro.com/nightly/linux/armhf/latest/`
- run RetroArch again, you should be able to download cores. 

### Online updater is still not working
You probably run RetroArch from the repository and it messed up your configs. You can try deleting the cfg file, but in my case it didn't helped. In that case:
- edit `~/.config/retroarch/retroarch.cfg`
- add or edit: `menu_show_online_updater = "true"`
- add or edit: `libretro_directory = "~/.config/retroarch/cores"`
- add or edit: `libretro_info_path = "~/.config/retroarch/cores"`
- look for other directory config lines which are trying to find files in the retroarch lib folder and edit them accordingly.

## Additional performance tweaks
- run `raspi-config`
- Advanced options -> GL Driver -> G2 GL (Fake KMS)
- save and reboot
