scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/zynq-7000.dtsi  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/pl.dtsi  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts/zynq-zed.dts  arch/arm/boot/dts
scp lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/configs/xilinx_zynq_defconfig arch/arm/configs
scp arch/arm/boot/dts/xilinx_zynq_defconfig lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/configs
scp arch/arm/configs/ lin@172.16.172.126:~/xilinx/linux-4.4.14/arch/arm/boot/dts

scp lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/configs/zynq_zed_defconfig u-boot/configs/
scp lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/include/configs/zynq-common.h u-boot/include/configs/
cp u-boot/configs/zynq_zed_defconfig lin@172.16.172.126:~/xilinx/u-boot-xlnx-xilinx-v2016.3/configs


export PATH=/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin:$PATH
export CROSS_COMPILE=arm-xilinx-linux-gnueabi-
export PATH=/home/lin/xilinx/u-boot-xlnx-xilinx-v2016.3/tools:$PATH

make ARCH=arm xilinx_zynq_defconfig
make ARCH=arm UIMAGE_LOADADDR=0x8000 uImage

make ARCH=arm dtbs
