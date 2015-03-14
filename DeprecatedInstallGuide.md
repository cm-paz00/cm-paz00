

# Installation Guide of CM-PAZ00 for Toshiba AC100 #

## Initial Install ##
### Prepare phase ###

---

<font color='red'><b>Backup all your valuable data to external storage before start</b> </font>

#### Simple path ####
  * Put zip files with cm-paz00 and [gapps](http://goo.im/gapps) to external sdcard formated to vfat fs
  * Flash `recovery.ac100-<current version>.img` to partition **#6 (aka LNX)** with _nvflash_ or _putusb_
```
    nvflash --bl bootloader.bin --download 6 recovery-<current version>.img --sync
```
#### Complex path ####
  * Restore original Toshiba's Android 2.1 backup
  1. Restore 2.1 partition table
  1. And flash whole content of partitions **#2 (aka BCT)**  and **#4 (aka EBT)**
  * Flash `recovery-<current version>.img` to partition **#5 (aka SOS)** with _nvflash_ or _putusb_
```
    nvflash --bl bootloader.bin --download 5 recovery-<current version>.img --sync
```
  * Put zip files with cm-paz00 and [gapps](http://goo.im/gapps) to external sdcard formated to vfat fs

### Install phase ###

---


#### For simple path ####
  * Boot device
  * Format all partitions except external sdcard
  * Choose flash file from sdcard and choose firmware zip then gapps zip
  * Reboot system

#### For complex path ####
  * Boot to recovery by holding _HOME_ key and pressing power, choose 1 on dialog
  * Format all partitions except external sdcard
  * Choose flash file from sdcard and choose firmware zip then gapps zip
  * Reboot system

## Update from previous version ##
  * Run wipe cache or factory reset (if factory reset you will lose all installed programs) from CMW-Recovery
  * Install new version zip from sdcard

# Resize default partition table #
Version starting from CM-10\_Beta4 require repartitioning of internal ac100 emmc,
to increase system and data partition sizes.

<font color='red'><b>Very important! Backup all your valuable data to external storage before start.</b> </font>

Download script from here https://github.com/zombah/ac100-simple-repart/archive/master.zip

## Resize from linux/unix os ##

---

  * Run simple-repart.sh
  * Follow steps one by one, backup fisrt, repartition second, restore third
  * Then follow install guide.


## Resize from win32/etc os ##

---

  * Run simple-repart.cmd
  * Follow steps one by one, backup fisrt, repartition second, restore third
  * Then follow install guide.

