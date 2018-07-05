---
title: ThePiGuy's Website
permalink: installing.html
description: Tutorials on how to install and build android
---
{% include navbar.html %}

# Installing a custom rom
## Installing a custom rom requires these basic steps
1. Unlock the bootloader - in the majority of cases, this will wipe all data
2. Install a custom recovery - the recommended variant for all devices is now TWRP
3. [Optional] Make a full twrp backup to allow you to easily return to stock if needed
4. Wipe System, Data, Cache and Dalvik in TWRP to remove the previous OS - internal storage contains files such as music, photos etc. These will NOT be backed up during a TWRP backup, so if you wipe this partition ensure you have these files backed up manually
5. Flash the ROM zip of your choice - ensure it is for the exact model you have as even devices with similar model names can have very different hardware
6. If applicable, flash the gapps package suitable for your device (I recommend [opengapps](https://opengapps.org/)) BEFORE rebooting into the OS - this ensures the gapps are fully embedded and prevents constant 'Google play services has stopped' errors
7. Reboot into system and enjoy
