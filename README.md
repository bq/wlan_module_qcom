WHAT IS THIS?
=============

Wlan module source code for the devices:
* bq aquaris E5 4G


BUILD INSTRUCTIONS?
===================

Specific sources are separated by releases with it's corresponding number. First, you should
clone the projects:

        $ git clone https://github.com/bq/aquaris-E5-4G.git ; git clone https://github.com/bq/wlan_module_qcom.git 

After it, choose the release you would like to build:

*Aquaris E5 4G*

        $ mv aquaris-E5-4G kernel ; cd kernel ; git checkout tags/{release} ; cd ..
        $ mv wlan_module_qcom wlan ; cd wlan ; git checkout tags/{release} ; cd ..

Download a prebuilt gcc according the next table of android versions:

| android                   | gcc                     |
| --------------------------|-------------------------|
| 4.4.4                     | 4.7                     |
| 5.0.2/5.1.1/6.0.1         | 4.8                     |


        $ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-{gcc}

Create KERNEL_OUT directory:

        $ mkdir KERNEL_OUT

Your directory tree should look like this:
* kernel
* arm-eabi-{gcc}
* KERNEL_OUT
* wlan

Build the kernel according the next table of product names:

| device                    | product                 |
| --------------------------|-------------------------|
| bq aquaris E5 4G          | vegetalte               |


        $ make -C kernel O=../KERNEL_OUT  ARCH=arm CROSS_COMPILE=../arm-eabi-{gcc}/bin/arm-eabi- {product}_defconfig
        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm CROSS_COMPILE=../arm-eabi-{gcc}/bin/arm-eabi-

You can specify "-j CORES" argument to speed-up your compilation, example:

        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm CROSS_COMPILE=../arm-eabi-{gcc}/bin/arm-eabi- -j 8

Finally, build the wlan module:

        $ make -C kernel/ M=../wlan/ O=../KERNEL_OUT/ ARCH=arm CROSS_COMPILE=../arm-eabi-{gcc}/bin/arm-eabi- modules WLAN_ROOT=../wlan/ MODNAME=wlan BOARD_PLATFORM=msm8916 CONFIG_PRONTO_WLAN=m

You can specify "-j CORES" argument to speed-up your compilation, example:

        $ make -C kernel/ M=../wlan/ O=../KERNEL_OUT/ ARCH=arm CROSS_COMPILE=../arm-eabi-{gcc}/bin/arm-eabi- modules WLAN_ROOT=../wlan/ MODNAME=wlan BOARD_PLATFORM=msm8916 CONFIG_PRONTO_WLAN=m -j 8

