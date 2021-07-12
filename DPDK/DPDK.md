# Mellanox ConnectX-5 Driver Installation
Linux Kernel version should be changed before installing driver.

Add `deb http://security.ubuntu.com/ubuntu trusty-security main` into `/etc/apt/sources.list`and run
```
sudo apt-get update
sudo apt-get install linux-image-4.15.0-147-generic
```
Then edit `/etc/default/grub` , set `GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.15.0-147-generic"` and reboot.


To install Mellanox ConnectX-5 driver on Ubuntu 18.04, run
```
wget https://content.mellanox.com/ofed/MLNX_OFED-4.9-2.2.4.0/MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64.tgz
tar -xvf MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64.tgz
cd MLNX_OFED_LINUX-4.9-2.2.4.0-ubuntu18.04-x86_64
sudo ./mlnxofedinstall --dpdk
sudo /etc/init.d/openibd restart # load the new driver
```
# DPDK Setup for Splinter/Kayak
`~/.cargo/config`
```
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'tuna'

[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"
```

Install the dependencies and DPDK with the following commands
```
sudo apt-get install curl libnuma-dev libpcap-dev clang libclang-dev libssl-dev pkg-config numactl
sudo ./get-dpdk.sh
```
Before running Kayak, you need to setup huge page:
Edit `/etc/default/grub` , set `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash iommu=pt intel_iommu=on default_hugepagesz=1GB hugepagesz=1G hugepages=16"`
Edit `/etc/fstab` , add `nodev /mnt/huge hugetlbfs pagesize=1GB 0 0"`

