NVIDIA Jetso TK1 exsample Yocto Distro


repo init -u https://github.com/watatuki/jetson-tk1-yocto-distro.git
repo sync

source poky/oe-init-build-env jetson-tk1-distro
bitbake jetson-tk1-image

