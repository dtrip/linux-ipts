### Linux with IPTS support
Linux Kernel 4.12 with Intel GPU-Accelerated Precise Touch & Stylus (IPTS) support. Basically to get touch screen working on my surface pro 4. I  have gone through and updated the drivers to integrate with the changes of the kernel from 4.90-rc3 to 4.12-rcA

I've included the module, firmware and patches to compile kernel. I've also included ubuntu mainline patches for building
as an Ubuntu kernel, however this should be able to be applied to all distro's. You will need the the [IPTS linux firmware](https://github.com/axelrtgs/linux-firmware-ipts) which can be found [here](https://github.com/axelrtgs/linux-firmware-ipts). An example to compile as an Ubuntu kernel:
```
$ git clone https://github.com/dtrip/linux-ipts ~/linux
$ cd ~/linux
$ patch -p1 -i 0001-base-packaging.patch
$ patch -p1 -i 
$ patch -p1 -i 
$ patch -p1 -i 
$ patch -p1 -i 
$ patch -p1 -i 
$ patch -p1 -i 
$ cp /boot/config-`uname -r` .config
$ chmod a+x debian/*
$ chmod a+x debian/scripts/*
$ chmod a+x debian/scripts/misc/*
$ fakeroot scripts/config --disable DEBUG_INFO
$ fakeroot scripts/config -m INTEL_IPTS
$ fakeroot scripts/config --disable MODULE_SIG
$ fakeroot scripts/config --disable SYSTEM_TRUSTED_KEYRING
$ fakeroot scripts/config --enable BLK_DEV_NAME
$ fakeroot scripts/config --set-val EXTRA_FIRMWARE_DIR 'firmware'
$ fakeroot scripts/config --set-val EXTRA_FIRMWARE 'intel/ipts/ipts_fw_config.bin'
$ fakeroot scripts/config --disable CFG80211_DEFAULT_PS
$ make oldconfig
$ fakeroot make-kpkg -j `getconf _NPROCESSORS_ONLN` 3 --initrd --append-to-version=-ipts kernel_image kernel-headers
% sudo dpkg -i ../linux-headers-4.12.0-rc1-ipts+_4.12.0-rc1-ipts+-10.00.Custom_amd64.deb ../linux-image-4.12.0-rc1-ipts+_4.12.0-rc1-ipts+-10.00.Custom_amd64.deb
```

Hopefully it builds successfully. I can say I was able to successfully build on my surface pro 4 running Ubuntu 16.10. I have uploaded the deb packages should you be wanting to simply install on another surface pro to get touch screen working (Note: you will still probably need the IPTS firmware as described [here](https://github.com/ipts-linux-org/ipts-linux-new/wiki))


## Many thanks
[ipts-linux-org](https://github.com/ipts-linux-org)

[jimdigriz](https://github.com/jimdigriz)

[fridgecow](https://github.com/fridgecow)

[axelrtgs](https://github.com/axelrtgs)
