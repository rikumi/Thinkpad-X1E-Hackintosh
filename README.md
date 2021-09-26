# Hackintosh for ThinkPad X1 Extreme Gen 1

![image](https://user-images.githubusercontent.com/5051300/134805178-c5422cb1-51fc-4ddc-9e8c-66c4ce25599a.png)

## Hardware Specs

- CPU: Intel Core i7-8750H
- GPU: Intel UHD Graphics 630 + GTX 1050 Ti (disabled for now)
- Memory: 8GB*2
- SSD: Samsung SSD 980 500GB (manually added) + Samsung PM981 512GB (disabled for now)
- Display: 3840x2160 with touch (touch not working yet)
- Wi-Fi & BT: Intel card (BT not working yet)

## What's working

- macOS Catalina 10.15.7
- Intel Wi-Fi card
- Speakers (Audio jack not tested)
- USB ports
- Fn & volume & brightness keys
- Touchpad with multi-touch

## What's not working

- Nvidia GPU
- Touch screen
- Primary SSD is disabled to prevent kernel panic
- No bluetooth
- HDMI port
- Waking from sleep is buggy
- Fingerprint reader
- IR camera is the default camera (don't try it at night)

## Offline Installation Guide for Windows

Here is a quick tip for installing macOS from Windows without either a Mac or Internet connection.

1. First use gibMacOS to download full installer image.
2. Use the `MakeInstall.bat` script from gibMacOS to create the bootable USB for Internet recovery.
3. Follow [this guide](https://www.reddit.com/r/hackintosh/comments/fdvf67/comment/fjjzrpm/) to create a `SharedSupport` folder. Do not follow the last step, since TransMac cannot identify the partition created by `MakeInstall.bat`.
4. Create an `exFAT` partition on one of your drives accessible by macOS Recovery. Copy the `SharedSupport` folder from last step into this exFAT partition.
5. Boot into Internet recovery with the USB. In recovery, open Terminal and run these commands to link SharedSupport into the Installer app:

```sh
mount -o rw -t hfs /dev/disk2s2 / # replace disk2s2 with your `macOS Base System` disk id
ln -s /Volumes/Shared/SharedSupport /Volumes/macOS\ Base\ System/Install\ macOS\ Catalina.app/Contents/ # replace Shared with your exFAT partition name
```

6. Now run the command to install the system:

```sh
/Volumes/macOS\ Base\ System/Install\ macOS\ Catalina.app/Contents/Resources/startosinstall --volume /Volumes/macOS
```

## Credits

Currently this is almost a copy of https://github.com/ergonyc/BlackMac-ThinkPad-X1E.

The SSDT_NVMe-Pcc.aml to disable primary NVMe SSD is borrowed from https://github.com/xuzhao9/ThinkPad-X1E-Hackintosh.

Also checkout https://github.com/Errrneist/Hackintosh-Thinkpad-X1-Extreme for his links to most of the related works.
