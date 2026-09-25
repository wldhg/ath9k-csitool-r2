# BPI-R2 Atheros CSITool Kernel

This is a Linux **5.4.12** kernel source for Banana Pi R2 (BPI-R2) which includes [Atheros CSI tool](https://github.com/xieyaxiongfly/Atheros-CSI-Tool).

### How To Build and Install?

#### A - Install Prebuilts

+ [Debian Image](https://www.dropbox.com/scl/fi/5c5uolnzutb90bsakjwnv/atheros-csitool.img.xz?rlkey=6jsz6tr7bsqjkqgf2048m2gyv&st=jplaytd1&dl=1) (Jan 09, 2020, 5.4.2 Kernel)\
  This image is a result of `dd` of 8GB sdcard and only kernel is installed. ID: `root` \ PWD: `bananapi`. I recommend you to install the *Build Output* below after install this image on your SD card.
+ [Debian Appready Image](https://www.dropbox.com/scl/fi/rkks7alwv0mviupx2mb1l/atheros-csitool-full.img.xz?rlkey=c59245ie259nymi5yvox125b8&st=zagdwxnm&dl=1) (Jan 11, 2020, 5.4.2 Kernel)\
  This is also an image of 8GB sdcard, and all prerequisites are installed. ID: `momo` \ PWD: `momo`.\
  Default shell is [fish](https://fishshell.com/) shell, you can change it to `bash` by typing `chsh momo /bin/bash`.\
  There is CSI-Collector app on home directory. To use them, `git pull` on that directory and read [this readme](https://github.com/wldhg/ath9k-csitool-apps).\
  I recommend you to install the *Build Output* below after install this image on your SD card.
+ [Build Output](https://github.com/wldhg/ath9k-csitool-r2/releases/tag/CI-CSITOOL-20200117_102218-b589f8da4) (Jan 17, 2020, 5.4.12 Kernel)\
  This is a latest csitool-runability-checked output of "pack" option at method B.

If you installed image file, after installation, you can extend your partition to the end of the sdcard using below commands in root shell:

```sh
apt-get install cloud-guest-utils
growpart /dev/mmcblk0 2
resize2fs /dev/mmcblk0p2
```

Check the installation with `dmesg | grep debug_csi`.

#### B - Build Yourself

On a x86/x64-host you need cross compile tools for the armhf architecture (`bison` and `flex` package are needed for kernels >=4.16):

```sh
sudo apt install ccache gcc-arm-linux-gnueabihf libc6-armhf-cross u-boot-tools bc make gcc libc6-dev libncurses5-dev libssl-dev bison flex
```

If you build it directly on the BananaPi-R2 you do not need the crosscompile-packages `gcc-arm-linux-gnueabihf` and `libc6-armhf-cross`

Then build using with default configuration:

```sh
./build.sh
```

The option "pack" creates a tar.gz-file which contains folders `BPI-BOOT` (content of boot-partition aka `/boot`) and `BPI-ROOT` (content for rootfs aka `/`).

Simply backup your existing `/boot/bananapi/bpi-r2/linux/uImage` and unpack the content of these 2 folders to your system.

You can also install direct to sd-card which makes a backup of kernelfile, here you have to change your `uEnv.txt` if you use a new filename (by default it's containing kernelversion.)

Finally, check the installation with `dmesg | grep debug_csi`.

### How To Get the CSI?

Look [here](https://github.com/wldhg/ath9k-csitool-apps#readme).

### Authors and License

- Base Linux Kernel: Linux Kernel Contributors, GPL-2.0, optimized and extended for BPI-R2 by [frank-w](https://github.com/frank-w).

- ath9k CSITool Driver: Yaxiong Xie ([Project Homepage](https://wands.sg/research/wifi/AtherosCSI/)).
