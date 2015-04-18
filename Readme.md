Arduino IDE 1.6.3 for Raspberry Pi
==================================

All credit goes to ShortTie who made this awesome patch.
This repository hosts the source with patches, compiled packages and additional instructions and notes.

See the post at the [Raspberry Pi Forum](https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=92662) for all information and support.

How to Install
==============

```bash

```

How to recompile
================

```bash

```

How to upgrade to a new IDE version
===================================

```bash

#get admin privilegs
sudo su

#create new working directory
mkdir Arduino
cd Arduino

#install quilt
apt-get install quilt
export QUILT_PATCHES=debian/patches
export QUILT_REFRESH_ARGS="-p ab --no-timestamps --no-index"

#download Arduino IDE and extract
wget https://github.com/arduino/Arduino/archive/1.6.3.zip
unzip -q 1.6.3.zip
cd Arduino-1.6.3/

#get arduino for debian and backup
wget http://ftp.de.debian.org/debian/pool/main/a/arduino/arduino_1.5.6.2+sdfsg2-3.debian.tar.xz
tar -xf arduino_1.5.6.2+sdfsg2-3.debian.tar.xz
cp -R debian debian.orig
cd debian

#download patch
wget https://www.dropbox.com/s/7m8gzlbxsh6psex/Raspbian.Arduino.arm.build.1.6.2.patch
patch -p1 < Raspbian.Arduino.arm.build.1.6.2.patch
rm Raspbian.Arduino.arm.build.1.6.2.patch
cd ..

quilt push
#correct error in patch, retry

#for fuzz:
quilt refresh

#for error
nano /debian/patches/file.patch

#after all errors are gone do
quilt pop -a
quilt push -a
quilt pop -a

#check if there are files ending with ~
ls -a debian/patches/
#if yes, delete them


#calculate the patch for other people
diff -ruN debian.orig debian > Raspbian.Arduino.arm.build.1.6.3.patch

```

