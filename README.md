WHAT IS THIS?
=============

Wlan module source code for the devices:
* bq aquaris X2


BUILD INSTRUCTIONS?
===================

Specific sources are separated by releases with it's corresponding number. First, you should
clone the projects:

        $ git clone https://github.com/bq/aquaris-X2.git ; git clone https://github.com/bq/wlan_module_qcom.git ; git clone https://github.com/bq/qca-wifi-host-cmn.git ; git clone https://github.com/bq/fw-api.git

After it, choose the release you would like to build:

*Aquaris X2*

        $ mv aquaris-X2 kernel ; cd kernel ; git checkout tags/{release} ; cd ..
        $ mv wlan_module_qcom wlan ; cd wlan ; git checkout tags/{release} ; cd ..
        $ mv qca-wifi-host-cmn ; cd qca-wifi-host-cmn ; git checkout tags/{release} ; cd ..
        $ mv fw-api ; cd fw-api ; git checkout tags/{release} ; cd ..


Download a prebuilt gcc:

        $ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9

Create KERNEL_OUT directory:

        $ mkdir KERNEL_OUT

Your directory tree should look like this:
* kernel
* aarch64-linux-android-4.9
* KERNEL_OUT
* wlan
* qca-wifi-host-cmn
* fw-api

Build the kernel according the next table of product names:

| device                    | product                 |
| --------------------------|-------------------------|
| bq aquaris X2             | zangya                  |


        $ make -C kernel O=../KERNEL_OUT ARCH=arm64 CROSS_COMPILE=../aarch64-linux-android-4.9 {product}_defconfig
        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm64 CROSS_COMPILE=../aarch64-linux-android-4.9/bin/aarch64-linux-android-

You can specify "-j{CORES}" argument to speed-up your compilation, example:

        $ make O=../KERNEL_OUT/ -C kernel ARCH=arm64 CROSS_COMPILE=../aarch64-linux-android-4.9/bin/aarch64-linux-android- -j8

Finally, build the wlan module:

        $ make -C kernel/ M=../wlan O=../KERNEL_OUT/ ARCH=arm64 CROSS_COMPILE=../aarch64-linux-android-4.9/bin/aarch64-linux-android- modules WLAN_ROOT=../wlan/ WLAN_COMMON_ROOT=../qca-wifi-host-cmn WLAN_COMMON_INC=../qca-wifi-host-cmn WLAN_FW_INC=../fw-api MODNAME=wlan BOARD_PLATFORM=sdm660 CONFIG_QCA_CLD_WLAN=m

You can specify "-j{CORES}" argument to speed-up your compilation, example:

        $ make -C kernel/ M=../wlan O=../KERNEL_OUT/ ARCH=arm64 CROSS_COMPILE=../aarch64-linux-android-4.9/bin/aarch64-linux-android- modules WLAN_ROOT=../wlan/ WLAN_COMMON_ROOT=../qca-wifi-host-cmn WLAN_COMMON_INC=../qca-wifi-host-cmn WLAN_FW_INC=../fw-api MODNAME=wlan BOARD_PLATFORM=sdm660 CONFIG_QCA_CLD_WLAN=m -j8

