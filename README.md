NVIDIA Jetson TK1 exsample Yocto Distro Scripts
====================================================================
These scripts aim at providing an exsample distro on Jetson TK1.
The Yocto Project is an open source collaboration project that provides templates, tools and methods to help you create custom Linux-based systems for embedded products regardless of the hardware architecture.
It does so by automating the process of cross-compiling the root filesystem.

Host System Preparation:
====================================================================
You need a install various packages.

exsample: Ubuntu12.04
sudo apt-get install sed wget subversion git-core coreutils unzip texi2html texinfo \
libsdl1.2-dev docbook-utils fop gawk python-pysqlite2 diffstat make gcc \
build-essential xsltproc g++ desktop-file-utils chrpath libgl1-mesa-dev \
libglu1-mesa-dev autoconf automake groff libtool xterm libxml-parser-perl

exsample: Ubuntu14.04
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
build-essential chrpath socat libsdl1.2-dev xterm make xsltproc docbook-utils \
fop dblatex xmlto autoconf automake libtool libglib2.0-dev


Target System Preparation:
====================================================================
You need a setup to boot from SD card at Jetson TK1.

Please proceed to the official guide of section 3.
http://developer.download.nvidia.com/embedded/L4T/r21_Release_v4.0/l4t_quick_start_guide.txt

At that time, you will need to replace command "sudo ./flash.sh ${BOARD} mmcblk0p1" to "sudo ./flash.sh 1jetson-tk1 mmcblk1p1".


Jetson TK1 exsample Yocto Distro
====================================================================
cd /path/to/work

repo init -u https://github.com/watatuki/jetson-tk1-yocto-distro.git

repo sync

source poky/oe-init-build-env jetson-tk1-distro

bitbake jetson-tk1-image



Install to SD card
====================================================================
SD card will assume that it is "/dev/sdx1".

sudo umount /dev/sdx1

sudo mkfs.ext4 /dev/sdx1

sudo mkdir -p /mnt/sdcard

sudo mount /dev/sdb1 /mnt/sdcard

cd /mnt/sdcard

sudo tar xvjf /path/to/work/jetson-tk1-distro/tmp/deploy/images/jetson-tk1-l4t/jetson-tk1-image-jetson-tk1-l4t.tar.bz2

sudo sync


