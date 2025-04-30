
# Getting Started
## **Step 1** - Download the Raspberry Pi Imaging Tool

**Official Download URL:** https://www.raspberrypi.com/software/
Supports Windows, macOS, Ubuntu, and Raspberry Pi OS systems
## **Step 2** - Configure the tool to image Alpine Linux

Select your Pi device, and then find the 64-bit version of Alpine Linux under "Other general-purpose OS". It should be compatible with all main Raspberry Pi and Zero boards.

![[rpi-imager-1.PNG]]
![[rpi-imager-2.PNG]]

## **Step 3** - Image your SD card and start your Pi

Since the image file size is tiny, imaging the SD card should be a very fast process. Once it is completed, load the card into your Raspberry Pi and connect the other necessary peripherals like a keyboard and display. If everything is working correctly, you should be greeted by the Alpine Linux login screen.

![[firstboot.PNG]]

## **Step 4** - Start to setup Alpine Linux
From here the steps to set up are extremely similar, so I will refer you to the [[Alpine Linux]] "Getting Started" section for most of this step. Return to Step 5 once you reach the setup stage "Disk & Install".
# Troubleshooting
## Low Resolution / No Resolution Options
### Possible Symptoms
 - Display is letterboxed, even in terminal mode
 - There is only one resolution option in display settings
### Possible Solutions
#### Update usercfg.txt with graphics settings

**usercfg.txt**
```
dtoverlay=vc4-fkms-v3d
max_framebuffers=2
```
