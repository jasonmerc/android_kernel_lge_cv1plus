1. Android build
  - Download original android source code ( android-7.1.2_r4  ) from http://source.android.com
    {
      $repo init -u git://10.168.177.185/platform/manifest.git -b android-7.1.2_r4
      $repo sync -cdq -j12 --no-tags
      $repo start android-7.1.2_r4 --all 
    )
  - Untar opensource packages of LMX212TA_Nougat_Android.tar.gz into downloaded android source directory
       a) tar -xvzf  LMX210MA_Nougat_Android.tar.gz
  - And, merge the source into the android source code
  - Run following scripts to build android
    a) source build/envsetup.sh
    b) lunch 1
    c) make -j4
  - When you compile the android source code, you have to add google original prebuilt source(toolchain) into the android directory.
  - After build, you can find output at out/target/product/generic

2. Kernel Build  
  - Uncompress using following command at the android directory
        a) tar -xvzf LMX212TA_Nougat_Kernel.tar.gz

  - When you compile the kernel source code, you have to add google original prebuilt source(toolchain) into the android directory.
  - Run following scripts to build kernel
  
    a) cd kernel
    b) mkdir -p out
	c) make ARCH=arm O=./out cv1_lao_com-perf_defconfig
	d) make ARCH=arm O=./out CROSS_COMPILE=$(pwd)/../../prebuilts/gcc/linux-x86/arm/arm-linux-androideabi-4.9/bin/arm-linux-androideabi- KERNEL_COMPRESSION_SUFFIX=gz -j4
	
	* "-j4" : The number, 4, is the number of multiple jobs to be invoked simultaneously. 
  - After build, you can find the build image(zImage) at out/arch/arm/boot

