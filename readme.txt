scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/zynq-7000.dtsi  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/pl.dtsi  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/zynq-zed.dts  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/configs/xilinx_zynq_defconfig arch/arm/configs
scp arch/arm/boot/dts/xilinx_zynq_defconfig lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/configs
scp arch/arm/configs/ lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts

scp lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/configs/zynq_zed_defconfig u-boot/configs/
scp lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/include/configs/zynq-common.h u-boot/include/configs/
scp u-boot/configs/zynq_zed_defconfig lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/configs

-make u-boot
make zynq_zed_defconfig
make 
scp lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/u-boot u-boot/


export PATH=/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin:$PATH
export CROSS_COMPILE=arm-xilinx-linux-gnueabi-
export PATH=/home/lin/xilinx/u-boot-xlnx-xilinx-v2016.3/tools:$PATH

make ARCH=arm xilinx_zynq_defconfig
make ARCH=arm UIMAGE_LOADADDR=0x8000 uImage

make ARCH=arm dtbs



linx u-boot编译
- 安装64位linux操作系统，只能Ubuntu 64 14.04
- 安装lib32

sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0

- 安装sdk

http://www.xilinx.com/support/download.html

- 设置环境变量

export PATH=/path/to/xilinx/arm/gnu/lin/bin:$PATH
export PATH=/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin:$PATH
export CROSS_COMPILE=arm-xilinx-linux-gnueabi-

- 安装openssl

sudo apt-get install libssl-dev
http://stackoverflow.com/questions/3016956/how-do-i-install-the-openssl-c-library-on-ubuntu

- 安装device-tree-compiler

sudo apt-get install device-tree-compiler
https://github.com/Koheron/zynq-sdk/issues/48

- 安装git

sudo apt-get install git

- 下载编译uboot

git clone https://github.com/Xilinx/u-boot-xlnx
make zynq_zed_defconfig
make

- 用sdk create boot image工具打包BOOT.bin

fsbl.elf + bit（可选）+ u-boot.elf

- 把BOOT.bin拷贝到SD卡中（FAT32文件系统），把启动模式跳线调整为SD卡启动（JP1-JP4 0101）
