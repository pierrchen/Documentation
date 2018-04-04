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
- Boot Poplar board from USB disk to the u-boot console
- Flash Partition Table and UEFI using
```
usb start;
fatload usb 0:1 ${scriptaddr} recovery_files/install.scr;
source ${scriptaddr}
```

5. Flash Android images

- Connect Poplar board to host PC with Type-A-Male to Type-A-Male cable
- Boot Poplar board from eMMC and Press "Escape" to enter UEFI Boot Menu
- Select "Boot Manager", select "Android Fastboot", press Enter.

Now, device enter into fastboot mode, you should see:

```
Android Fastboot mode - version 0.6.
Press RETURN or SPACE key to quit.
```

- Check if device is in fastboot mode On host

```
$sudo fastboot devices
247BB42E70735797	fastboot
```

- Flash
```
cd $OUT
sudo fastboot flash mmcsda2 boot.img
sudo fastboot flash mmcsda3 system.img
sudo fastboot flash mmcsda5 cache.img
sudo fastboot flash mmcsda6 userdata.img
```

6. Reboot, and Android should be booted up.