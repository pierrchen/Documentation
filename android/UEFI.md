1. Dependency for building UEFI

```
sudo apt-get install uuid-dev
```

2. Clone UEFI repositories

```
$ mkdir -p device/hisilicon/bootloader
$ cd device/hisilicon/bootloader
$ git clone https://github.com/ARM-software/arm-trusted-firmware
$ git clone https://github.com/96boards-poplar/edk2.git
$ git clone https://github.com/96boards-poplar/OpenPlatformPkg.git
```

3. Build UEFI in Android environment

```
$ cd android_root_directory
$ source build/envsetup.sh && lunch poplar-eng
$ cd device/hisilicon/poplar/bootloader
$ make
```

4. Install UEFI to Poplar board

- Copy device/hisilicon/poplar/l-loader/installer/* to USB disk
- Boot Poplar board from USB disk
- Partition table and UEFI will be installed to eMMC automatically

5. Flash Android images

- Connect Poplar board to host PC with Type-A-Male to Type-A-Male cable
- Boot Poplar board from eMMC, and UEFI should boot into fastboot mode
automatically
- Run device/hisilicon/poplar/l-loader/installer/flash-all.sh on host PC

6. Reboot, and Android should be booted up.