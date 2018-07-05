---
title: ThePiGuy's Website
permalink: installing.html
description: Tutorials on how to install and build android
---
{% include navbar.html %}

# Installing a custom rom
## Installing a custom rom requires these basic steps (more detailed steps below)
1. Unlock the bootloader - in the majority of cases, this will wipe all data
2. Install a custom recovery - the recommended variant for all devices is now TWRP
3. [Optional] Make a full twrp backup to allow you to easily return to stock if needed
4. Wipe System, Data, Cache and Dalvik in TWRP to remove the previous OS - internal storage contains files such as music, photos etc. These will NOT be backed up during a TWRP backup, so if you wipe this partition ensure you have these files backed up manually
5. Flash the ROM zip of your choice - ensure it is for the exact model you have as even devices with similar model names can have very different hardware.
If you experience "Error 7" whilst using an Oreo rom, ensure your TWRP is the latest version
6. If applicable, flash the gapps package suitable for your device (I recommend [opengapps](https://opengapps.org/)) BEFORE rebooting into the OS - this ensures the gapps are fully embedded and prevents constant 'Google play services has stopped' errors
7. Reboot into system and enjoy

## Installing in more detail
The bootloader unlocking step varies from device to device, so I will explain the normal method, followed by the LG specific way (I am an LG owner)

### Install platform tools
Platform tools contain the adb and fastboot packages that are needed to unlock the bootloader

The way you install these tools depends on the operating system running on your PC

#### Windows
1. Download the [windows platform-tools package](https://dl.google.com/android/repository/platform-tools-latest-windows.zip) from Google and extract it into a directory of your choice. C:\Users\\[Username]\platform-tools\ is always a good place
2. We will now modify the path variable to allow you to access the tools from any directory. Open up the start menu and search for path. Click on "Edit the system environment variables". Then click on "Environment Variables" near the bottom. In the box under "User variables for [Username]", double click on the bar that has "Path" on the left hand side. Then click "New" and type in the path to (and including) the platform-tools. E.g. if you had it placed in C:\Users\\[Username]\platform-tools\, then that is what you would type into the box. Then hit enter/return on the keyboard and then "Ok" on the window. Now adb and fastboot should be accessible in CMD from any location.

#### Linux
1. Download the [linux platform-tools package](https://dl.google.com/android/repository/platform-tools-latest-linux.zip) from Google and extract it into a directory of your choice. /home/[Username]/platform-tools/ is always a good place.
2. We will now add this to the ~/.profile file to make it executable from any directory. Add the following code to ~/.profile

```
# add Android SDK platform tools to path
if [ -d "$HOME/platform-tools" ] ; then
    PATH="$HOME/platform-tools:$PATH"
fi
```

Save the file. Now adb and fastboot should be accessible from any directory
3. You will now need to set up your udev rules to give ownership of your device to you. This website [here](http://www.janosgyerik.com/adding-udev-rules-for-usb-debugging-android-devices/) explains how to add udev rules for your device. Be aware that you will need different ones for the OS and bootloader mode.

### Unlock the bootloader
Now we need to enable the android debugging bridge (adb) and allow OEM unlocking in the stock OS in order to allow us to unlock the bootloader

1. Open settings
2. Go to About Phone (it might be under System)
3. Find the build number in that menu (it varies from device to device so it might be in a submenu in there)
4. Tap it 7 times (it should pop up saying developer options are enabled)
5. Now go to Developer Options (it will have just appeared)
6. Enable them if they aren't already and find and enable "OEM Unlocking"
7. Find and enable ADB
8. On your PC, run ```adb devices``` and click allow on the popup on your phone's screen
9. Now run ```adb reboot bootloader```
We should now reboot into the bootloader/fastboot mode

#### Google, OnePlus etc (the normal way)
Run ```fastboot flashing unlock``` (Google) or ```fastboot oem unlock``` (Oneplus, older Google and many others). This will factory reset your device and unlock your bootloader

#### LG
##### For European devices (G4 and newer)
These can be officially unlocked through the [LG Official Bootloader unlocking tool](https://developer.lge.com/resource/mobile/RetrieveBootloader.dev?categoryTypeCode=ANRS)

##### T-Mobile Devices
These can usually be unlocked using the ```fastboot oem unlock``` command (like Google and others)

##### Other devices
I only know about the G4 (feel free to put a pull request on my [website repo](https://github.com/thepiguy0/thepiguy0.github.io) to add other devices to this)

H810, H812, non-european H815, vs986 - Use the [UsU tool](https://forum.xda-developers.com/g4/general/unlock-unlock-lg-g4-device-usu-t3760451) from steadfasterX on XDA

### IMPORTANT - Make the TWRP install permanent
For most officially unlocked devices (hacks like the UsU may be different), we need to boot directly into twrp first to allow it to patch our current rom.

1. Find the recovery key combination for your device (e.g. LG G4 is power + volume down until LG logo appears, then briefly release and then hold down the power button without releasing the volume button and then hold both buttons until factory reset screen appears. Press yes twice and then you should boot into twrp)
2. Run ```fastboot reboot```
3. As soon as the screen goes black, perform this key combo as though you are turning on the device
4. Once you boot into twrp, allow it to make system modifications

### Now follow the basic steps above to finish installing your custom rom
