

# Installation Guide of CM-PAZ00 for Toshiba AC100/Dynabook AZ starting from version CM-10.1 #

## Initial Install ##
### Prepare phase ###

---

<font color='red'><b>!!!Backup all your valuable data to external storage before start!!!</b> </font>

#### Download ####
  * Download cm\_ac100-ota-10.1.zip and recovery-cm-10.1.img files, link below
    1. [External Downloads](https://drive.google.com/folderview?id=0BzHUnWusu2ztWl8yT2h3LXgxTmc&usp=sharing) <br>
</li></ul><ul><li>Download sos-uboot.bin latest version, link below<br>
<ol><li><a href='https://drive.google.com/folderview?id=0BzHUnWusu2ztWl8yT2h3LXgxTmc&usp=sharing'>External Downloads</a> <br>
</li></ol></li><li>Download nvflash or tegrarcm if you dont have one, for your pc platform, some links below<br>
<ol><li><a href='http://nv-tegra.nvidia.com/gitweb/?p=tools/tegrarcm.git;a=summary'>tegrarcm source repo</a>
</li><li><a href='http://mirror.yandex.ru/debian/pool/non-free/t/tegrarcm/'>tegrarcm binaries</a>
</li><li><a href='http://ac100.grandou.net/nvflash#debian_ubuntu_package'>nvflash debian</a>
</li><li><a href='http://paz00.ru/index.php/File:Nvflash-win.zip'>nvflash windows binary</a>
</li><li><a href='https://www.dropbox.com/s/8dwnsj4m2ksb4bw/linux4tegra.zip'>nvflash linux4tegra</a>
</li></ol></li><li>Download Google Apps package if you need one for appropriate release, link for non neon pack below<br>
<ol><li><font color='red'><b>!!!Use Gapps for exact system version, otherwise you may encounter problems like no icons on desktop, etc!!!</b> </font>
</li><li><a href='http://yadi.sk/d/yCrCGgqfC6Xvp'>CM-10.1 NON-NEON Gapps mirror</a>
</li><li><a href='http://yadi.sk/d/MR_aUFCgDcAsT'>CM-10.2 NON-NEON Gapps mirror</a>
</li><li><a href='http://yadi.sk/d/tkRraxinKCtpZ'>CM-11.0 NON-NEON Gapps mirror</a></li></ol></li></ul>

#### Prepare external SD card ####
  * Copy cm\_ac100-ota-10.1.zip, recovery-cm-10.1.img and gapps-non-neon.zip to VFAT/FAT32 formated external SD card

#### Setup PC ####
  * Copy nvflash/tegrarcm and sos-uboot.bin to some folder on your pc

#### Prepare AC100 ####
  * <font color='red'><b>Insert external SD card to your AC100</b> </font>
  * Connect AC100 mini-usb port with your PC with appropriate cable
  * Run AC100 in APX/recovery mode
    1. Press and hold CTRL+ESC+POWER keys at the same time
  * Check your PC log that AC100 running in APX mode
    1. Linux syslog example
```
    2013-10-25T01:39:24.294010+04:00 stallion kernel: [10308.101230] usb 2-1.2: new high-speed USB device number 20 using ehci-pci
    2013-10-25T01:39:24.380000+04:00 stallion kernel: [10308.187310] usb 2-1.2: New USB device found, idVendor=0955, idProduct=7820
    2013-10-25T01:39:24.380050+04:00 stallion kernel: [10308.187331] usb 2-1.2: New USB device strings: Mfr=1, Product=2, SerialNumber=0
    2013-10-25T01:39:24.380057+04:00 stallion kernel: [10308.187335] usb 2-1.2: Product: APX
    2013-10-25T01:39:24.380061+04:00 stallion kernel: [10308.187338] usb 2-1.2: Manufacturer: NVIDIA Corp.
```

### Switch to U-Boot bootloader and GPT partition table ###

---


#### If you use nvflash ####
  * If your AC100 in APX mode, run
```
   cd /path/to/your/nvflash_and_sos-uboot/location
   ./nvflash --bl sos-uboot.bin --go
```

#### If you use tegrarcm ####
  * Create bct file for your AC100 version
    1. Search for instructions in internet if you dont know what it is or ask at #ac100 freenode channel
  * If your AC100 in APX mode, run
```
   cd /path/to/your/tegrarcm_and_sos-uboot/location
   ./tegrarcm --bct=your.bct --bootloader=sos-uboot.bin --loadaddr=0x108000
```

  * Succsesfull output must look like this
```
bct file: ac100.bct                                                                                                                                                            
booloader file: sos-uboot-r5-2013-09-23.bin                                                                                                                                    
load addr 0x108000                                                                                                                                                             
entry addr 0x108000                                                                                                                                                            
device id: 0x7820                                                                                                                                                              
uid:  0x161c110341ffb597                                                                                                                                                       
RCM version: 2.1                                                                                                                                                               
downloading miniloader to target...
miniloader downloaded successfully
Chip UID:                0x0000000000000000161c110341ffb597
Chip ID:                 0x20
Chip ID Major Version:   0x1
Chip ID Minor Version:   0x2
Chip SKU:                0x8 (t20)
Boot ROM Version:        0x1
Boot Device:             0x2 (EMMC)
Operating Mode:          0x3 (developer mode)
Device Config Strap:     0x0
Device Config Fuse:      0x0
SDRAM Config Strap:      0x0
sending file: ac100.bct
- 4080/4080 bytes sent
ac100.bct sent successfully
sending file: sos-uboot-r5-2013-09-23.bin
- 6586773/6586773 bytes sent
sos-uboot-r5-2013-09-23.bin sent successfully
```

#### Run sos-uboot ####
  * U-Boot boot menu will appear on AC100 screen
    1. Choose **Boot Kernel** option and press ENTER
  * You must see shell prompt after
```
/ #
```

#### Runs switch-to-uboot ####
  * If your AC100 already run U-Boot bootloader and GPT partition table skip this step
  * In shell prompt run switch-to-uboot script
```
./switch-to-uboot
```
  * Answer yes to question prompt
  * After script finish it work check that process went fine, with running parted command
```
parted /dev/mmcblk1 print
```
  * Output must look like this, for 8Gb device already reparted for beta4
```
Model: MMC SEM08G (sd/mmc)
Disk /dev/mmcblk1: 7944MB
Sector size (logical/physical): 512B/512B
Partition table: gpt
Disk Flags:
 
Number  Start   End      Size    File system  Name   Flags
 1      3670kB  8913kB   5343kB  ext2         SOS
 2      8913kB  17.3MB   8389kB  ext2         LNX
 3      18.4MB  556MB    537MB   ext4         APP
 4      556MB   975MB    419MB   ext4         CAC
 5      975MB   977MB    2097kB               MSC
 6      978MB   5172MB   4194MB  ext4         UDA
 7      5173MB  7942MB   2769MB               UDB
```


#### Create new partition table ####
  * Use GNU parted to resize tables or create new one
  * For CM-10.1 or later android it is important to keep old partitions count as they written in Android fstab file
  * Delete your current partitions, choose the ones you want to modify
```
parted /dev/mmcblk1 rm 7 rm 6 rm 5 rm 4 rm 3 rm 2 rm 1
```
  * Or clean partition table at all
```
parted /dev/mmcblk1 mklabel gpt
```
  * Here some examples of new partition table
    1. If you plan to run only Android on your AC100
```
parted /dev/mmcblk1 -s mkpart primary 7168s 132168s 
parted /dev/mmcblk1 -s mkpart primary 132169s 257169s
parted /dev/mmcblk1 -s mkpart primary 257170s 1257170s
parted /dev/mmcblk1 -s mkpart primary 1257171s 2257171s
parted /dev/mmcblk1 -s mkpart primary 2257172s 2261078s
parted /dev/mmcblk1 -s mkpart primary 2261079s 15513695s
parted /dev/mmcblk1 -s name 1 SOS name 2 LNX name 3 APP name 4 CAC name 5 MSC name 6 UDA
parted /dev/mmcblk1 unit s print
```
    1. If you plan to run Android and Linux multiboot
```
parted /dev/mmcblk1 -s mkpart primary 7168s 132168s 
parted /dev/mmcblk1 -s mkpart primary 132169s 257169s
parted /dev/mmcblk1 -s mkpart primary 257170s 1257170s
parted /dev/mmcblk1 -s mkpart primary 1257171s 2257171s
parted /dev/mmcblk1 -s mkpart primary 2257172s 2261078s
parted /dev/mmcblk1 -s mkpart primary 2261079s 7698579s
parted /dev/mmcblk1 -s mkpart primary 7698580s 15513695s
parted /dev/mmcblk1 -s name 1 SOS name 2 LNX name 3 APP name 4 CAC name 5 MSC name 6 UDA name 7 UDB
parted /dev/mmcblk1 unit s print
```

  * Format new partitions
```
mkfs.ext2 /dev/mmcblk1p1
mkfs.ext2 /dev/mmcblk1p2
mkfs.ext4 /dev/mmcblk1p3
mkfs.ext4 /dev/mmcblk1p4
mkfs.ext4 /dev/mmcblk1p6
mkfs.ext4 /dev/mmcblk1p7
```

### Install CWM recovery for CM-10.1 ###
  * This must be done in sos-uboot running after you formated partitions
  * Create mount point for External SD card
```
mkdir /tmp/sd
```
  * Create mount point for SOS partition
```
mkdir /tmp/p1
```
  * Mount External SD card
```
mount /dev/mmcblk0p1 /tmp/sd
```
  * Mount SOS partition
```
mount /dev/mmcblk1p1 /tmp/p1
```
  * Create boot folder on SOS partition
```
mkdir /tmp/p1/boot
```
  * Unzip CWM kernel and ramdisk to SOS partition
```
unzip /tmp/sd/recovery-10.1.img -d /tmp/p1/boot/
```
  * Check that files copied fine
```
ls -la /tmp/p1/boot
```
  * Sync copied data
```
sync
```
  * Unmount External SD card and SOS
```
umount /tmp/sd
umount /tmp/p1
```
  * Press and hold POWER button to shutdown
    1. sos-uboot reboot and halt commands not working yet

### CM-10.1 ota file install ###
  * Turn on your AC100 with POWER button press
  * U-Boot Boot menu will appear on your AC100 screen
  * Choose **Boot SOS CM-10.1** option with direction keys and press ENTER
  * CWM recovery will boot
  * Choose **install zip** option from menu with direction keys and press ENTER
  * Choose **choose zip from sdcard** option
  * Choose **cm\_ac100-ota-cm-10.1.zip** file and press ENTER
  * Choose **Yes - Istall** from menu
  * Repeat same for GAPPS if needed
  * Choose **reboot system now** from CWM main menu
  * On U-Boot Boot menu screen choose **Boot LNX CM-10.1**


---


## Update recovery ##

  * <font color='red'>**Remeber to use same version for recovery and system </font>
  ***<font color='red'>