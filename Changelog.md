# <font color='blue'>Changelog</font> #

---

## CM-11.0-20140322-UNOFFICIAL ##
  * Based on current CM-11.0
    1. SELinux enabled
    1. Headset detection fixed

## CM-11.0-20140309-UNOFFICIAL ##
  * Based on CM-11.0-M4
  * First build, not tested yet
    1. SELinux not working
    1. 3G DHCP problems
    1. Many things can still be broken

## CM-10.2-20131109-UNOFFICIAL ##
  * Based on CM-10.2-M1
  * <font color='red'>Test version<br>
<ol><li>Visual artifacts<br>
</li><li>SELinux not working<br>
</li><li>Many things can be broken<br>
</font></li></ol>

## CM-10.1-20131103-UNOFFICIAL ##
  * Switch to U-Boot
  * Switch to GPT partition table
  * based on cm-10.1 current branch
  * Known problems
    1. Video recording in Camera app not working
    1. Suspend not working

## CM-10\_Beta4 ##
  * Kernel updated to rel15r7
  * Wifi drivers changed to compat-wireless 3.2.5-1
  * Edge leds work with lid closed
  * OTA Updater replaced with native CMUpdater
  * Persistent wakelock to prevent broken suspend freezes
  * disablesuspend.sh/enablesuspend.sh for totaly disable suspend features
  * Partial u-boot support
  * Various small fixes

## CM10\_Beta3 ##
  * Based on CM10 release branch jellybean-stable
  * Various small fixes

## CM10\_Beta2 ##
  * wpa\_supplicant changed to bcmhd version
  * LegacyCamera.apk application added
  * abootimg android port added
  * Small fonts footprint to lower system size
  * Some outdated apps removed
  * Legacy audio blob patch switched from custom to cm bundled

## CM10\_Beta1 ##
  * Initial release
  * Wifi enabled
  * Sound routing enabled
  * Accelerated video decoding enabled
  * MTP now default usb gadget mode

## Beta 3\_1 ##
  * Power Management script added to init.d, name /system/etc/init.d/02PmStuff
  * Useless reboot options removed (reboot to recovery, reboot to bootloader)
  * Gnu screen binary added

## Beta 3 ##
  * Nvidia blobs updated to 05.21.2012 Ventana version
  * One firmware now support all models cmdline
  * OTAUpdate tag changed to ac100, update notification from previous versions not supported
  * wwlan-select script added, to auto detect internal or external 3g modem (**borrowed from adam build**)
  * mkfs.vfat binary included
  * Kenel: switched to lzma compression, joysticks support turned on
  * TouchPad config file included, default touchpad cursor switched to pointer
  * Powerbutton behavior switched to single click power button menu, suspend on power button disabled until fixed

## Beta 2 ##
  * Internal mic routing fixed. Must work in applications now
  * Headphones routing fixed. Speakers will turn off when headphones connected
  * Visit Settings->Launcher->Homescreen->Grid size->Ok to fix icons placed out of homescreen (temp solution)
  * Kernel: fb flip removed, default brightness lowered, ppp modules included
  * OTAUpdater added for test (**edgi** will support it)
  * 117 suffix version changed from tegrapart to nvtegra\_hideparts

## Beta 1 ##

  * Move to ics-release cyanogenmod branch
  * **Gormar** fixes for vold, modem and keyboard
  * Power menu with double click on power button (temp solution)
  * Correct battery capacity status (temp solution)
  * Switch to tinyhal
  * No preempt kernel to fix nvec freezes
  * **Savalik** corrected keylayout for nvec\_keyboard
  * rukeyboard IME included to firmware with author permission (Thanks to    **vovkab**)