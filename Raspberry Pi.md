# Troubleshooting
## Power Supply

Power supply issues are common on the Raspberry Pi and could be the source of seemingly unrelated malfunctions. Even if your AC-to-USB adapter technically can provide enough wattage, it may not actually be delivering the device sufficient power for it to pass onto its peripherals, or even to run stably.

### Possible Symptoms

- Pi's power LED does not turn on (note: Pi Zero v1.3 does not have a power LED, but v2 does)
- Under-voltage warning on display (yellow lightning bolt icon)
- Peripherals do not power up completely or at all
- Mouse and/or keyboard suddenly stop responding in desktop environment

### Possible Solutions

This section contains some methods that might solve power supply issues.
#### Avoid Chaining Power Supply Hubs

It's possible that chaining certain power supply hubs together could cause issues. For example, powering the Pi from a USB hub that is in turn plugged into an AC power strip. Supplying the Pi with a dedicated AC-to-USB adapter directly from the power strip could resolve power supply issues.
#### Use the Official Raspberry Pi Power Supply

It's annoying to need a special power supply, but the compatibility is guaranteed.

**USB-C Version (Raspberry Pi 5):**
- [PiShop.us](https://www.pishop.us/product/raspberry-pi-27w-usb-c-power-supply-black-us/?searchid=0)
- [Adafruit](https://www.adafruit.com/product/5814)
- [Amazon](https://www.amazon.com/XYGStudy-Official-USB-C-Supply-Raspberry/dp/B0CQV29QSX)
**Micro-USB Version (Most Others):**
- [PiShop.us](https://www.pishop.us/product/raspberry-pi-12-5w-power-supply-us-white/?searchid=0)
- [Adafruit](https://www.adafruit.com/product/1995)
- [Amazon](https://www.amazon.com/KidsRobot-Raspberry-Official-Adapter-Support/dp/B09XN7H9M8)
#### Configure Power Settings

> [!warning]
> **Try this one at your own risk!**
> 
> At time of writing (4/29/2025) I have only tried this once, but I can say it solved a mouse & keyboard freezing issue I had with a Pi Zero 2 W running Alpine Linux with XFCE desktop environment. It seemed to generally improve the responsiveness of the device as well, and has not burnt it up so far.

In the [Pi's config.txt or usercfg.txt](https://www.raspberrypi.com/documentation/computers/config_txt.html), increase the upper voltage limit provided to the CPU and GPU:

**usercfg.txt**
```
over_voltage=2
force_turbo=1
```
This should prevent malfunctions related to under-voltage of the main processors.