# Mellanox ConnectX-5 Driver Installation
To install Mellanox ConnectX-5 driver on Ubuntu 18.04, run
```
wget https://content.mellanox.com/ofed/MLNX_OFED-4.9-2.2.4.0/MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64.tgz
tar -xvf MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64.tgz
cd MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64
sudo ./mlnxofedinstall --dpdk
sudo /etc/init.d/openibd restart # load the new driver
```
# DPDK Setup
Linux Kernel version should be changed before compiling DPDK.

Add `deb http://security.ubuntu.com/ubuntu trusty-security main` into `/etc/apt/sources.list`and run
```
sudo apt-get update
sudo apt-get install linux-image-4.15.0-147-generic
```
Then edit `/etc/default/grub` , set `GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.15.0-147-generic"` and reboot.

After that, install the dependencies and DPDK with the following commands
```
sudo apt-get install curl libnuma-dev libpcap-dev
sudo ./get-dpdk.sh
```
