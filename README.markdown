Android Open Source Project for HP Touchpad
===========================================

This README documents instructions to build Android for HP Touchpad.  
*Last updated:* 13th March 2012

Copyright (C) 2012 Wong Yong Jie  
Copyright (C) 2012 The Android Open Source Project

Build Requirements
------------------

The build requirements for Android 4.0 (Ice Cream Sandwich) is considerably  
higher than previous versions. For fast builds, powerful hardware is required.

The Android build system can take advantage of multiple cores to speed up the  
build process. However, you will need to ensure that you have sufficient memory  
installed so that the build process will not trash the disk / fail.

*Recommended:*  
* Core 2 Quad / Core i7 class CPUs  
* At least 8 GB of RAM

*Operating system configuration:*
Refer to [Initializing a Build Environment](http://source.android.com/source/initializing.html).

Build Instructions
------------------

1. Refer to [Downloading the Source Tree](http://source.android.com/source/downloading.html) to
   download the sources.

2. Copy the following local manifest to .repo/local\_manifest.xml.

--- cut here ---
``` xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>

  <remote  name="github"
           fetch="git://github.com/" />

  <remote  name="caf"
           fetch="git://codeaurora.org/" />

  <!-- CM overrides -->
  <remove-project name="platform/build" />
  <project path="build" name="CyanogenMod/android_build" remote="github" revision="ics">
    <copyfile src="core/root.mk" dest="Makefile" />
  </project>
  <remove-project name="platform/bionic" />
  <project path="bionic" name="CyanogenMod/android_bionic" remote="github" revision="ics" />
  <remove-project name="platform/bootable/bootloader/legacy" />
  <project path="bootable/bootloader/legacy" name="CyanogenMod/android_bootable_bootloader_legacy" remote="github" revision="ics" />
  <remove-project name="platform/bootable/diskinstaller" />
  <project path="bootable/diskinstaller" name="CyanogenMod/android_bootable_diskinstaller" remote="github" revision="ics" />
  <remove-project name="platform/bootable/recovery" />
  <project path="bootable/recovery" name="CyanogenMod/android_bootable_recovery" remote="github" revision="ics" />
  <remove-project name="platform/dalvik" />
  <project path="dalvik" name="CyanogenMod/android_dalvik" remote="github" revision="ics" />
  <remove-project name="platform/external/yaffs2" />
  <project path="external/yaffs2" name="CyanogenMod/android_external_yaffs2" remote="github" revision="ics" />
  <remove-project name="platform/external/skia" />
  <project path="external/skia" name="CyanogenMod/android_external_skia" remote="github" revision="ics" />
  <remove-project name="platform/external/wpa_supplicant_6" />
  <project path="external/wpa_supplicant_6" name="CyanogenMod/android_external_wpa_supplicant_6" remote="github" revision="ics" />
  <remove-project name="platform/libcore" />
  <project path="libcore" name="CyanogenMod/android_libcore" remote="github" revision="ics" />
  <remove-project name="platform/system/bluetooth" />
  <project path="system/bluetooth" name="CyanogenMod/android_system_bluetooth" remote="github" revision="ics" />
  <remove-project name="platform/system/core" />
  <project path="system/core" name="teamhacksung/android_system_core" remote="private" revision="ics" />
  <remove-project name="platform/system/extras" />
  <project path="system/extras" name="CyanogenMod/android_system_extras" remote="github" revision="ics" />
  <remove-project name="platform/system/media" />
  <project path="system/media" name="CyanogenMod/android_system_media" remote="github" revision="ics" />
  <remove-project name="platform/system/netd" />
  <project path="system/netd" name="CyanogenMod/android_system_netd" remote="github" revision="ics" />
  <remove-project name="platform/system/vold" />
  <project path="system/vold" name="CyanogenMod/android_system_vold" remote="github" revision="ics" />

  <!-- CM additional hardware support -->
  <project path="hardware/cm" name="CyanogenMod/android_hardware_cm" remote="github" revision="ics" />
  <remove-project name="platform/hardware/libhardware" />
  <project path="hardware/libhardware" name="CyanogenMod/android_hardware_libhardware" remote="private" revision="ics" />
  <remove-project name="platform/hardware/libhardware_legacy" />
  <project path="hardware/libhardware_legacy" name="CyanogenMod/android_hardware_libhardware_legacy" remote="github" revision="ics" />
  <remove-project name="platform/hardware/ril" />
  <project path="hardware/ril" name="CyanogenMod/android_hardware_ril" remote="github" revision="ics" />
  <project path="external/alsa-lib" name="CyanogenMod/android_external_alsa-lib" remote="github" revision="gingerbread" />

  <!-- Busybox support -->
  <project path="external/busybox" name="CyanogenMod/android_external_busybox" remote="github" revision="ics" />

  <!-- Superuser support -->
  <project path="system/su" name="CyanogenMod/android_system_su" remote="github" revision="ics" />
  <project path="packages/apps/Superuser" name="CyanogenMod/android_packages_apps_Superuser" remote="github" revision="ics" />

  <!-- Google Apps support -->
  <project path="vendor/google" name="yjwong/android_vendor_google" remote="private" revision="ics" />

  <!-- AOSP for HP Touchpad -->
  <project path="kernel/hp/tenderloin" name="yjwong/android_kernel_hp_tenderloin" remote="github" revision="ics" />
  <project path="device/hp/tenderloin" name="yjwong/android_device_hp_tenderloin" remote="github" revision="ics" />
  <project path="vendor/hp" name="yjwong/android_proprietary_hp" remote="github" revision="ics" />
  <project path="hardware/qcom/display" name="CyanogenMod/android_hardware_qcom_display" remote="github" revision="ics" />
  <project path="hardware/qcom/camera" name="yjwong/android_hardware_qcom_camera" remote="github" revision="ics" />
  <remove-project name="platform/hardware/qcom/media" />
  <project path="hardware/qcom/media" name="yjwong/android_hardware_qcom_media" remote="github" revision="ics" />
  <project path="hardware/atheros" name="yjwong/android_hardware_atheros" remote="github" revision="ics" />

</manifest>
```
--- cut here ---

3. Run `. build/envsetup.sh` to setup the build environment.

4. Run `repo sync -jN` (replace N with the number of parallel jobs).

5. Run `. build/envsetup.sh` to refresh the list of buildable devices.

6. Run `lunch` to obtain the list buildable devices.
   Choose full\_tenderloin-CFG where CFG is either eng, userdebug or user.

7. Run `make -jN otapackage` (replace N with the number of parallel jobs).

At this stage, hopefully the build will proceed without any errors.  
Output files will be found in out/target/product/tenderloin/full\_tenderloin-CFG.zip

The resultant ZIP file is a ClockworkMod flashable ZIP.

