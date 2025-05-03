# Getting Started

In this guide we will be setting up Ubuntu Desktop 24.04.2 LTS on a virtual machine. I will be using Oracle VirtualBox Manager on a Windows 10 Professional host, but the steps should be the same for other virtual machine hosts or even actual hardware.
## Requirements

**Official Downloads:**
https://ubuntu.com/download/desktop

The exact system requirements for each version are listed on the downloads page.

For this example setup I will create a virtual machine with double the system requirements:

| Requirement     | VM       |
| --------------- | -------- |
| 2 CPUs (2 GHz+) | 4 CPUs   |
| 4 GB RAM        | 8 GB RAM |
| 25 GB HD        | 50 GB HD |
I will be giving the VM internet access so that Ubuntu can make updates.

>[!note] Ubuntu 25 Supports ARM64
Interestingly, Ubuntu 25 can run on ARM64 processors. Possibly on a [[Raspberry Pi]]?

## Setup

Using the downloads page above, download the latest version of Ubuntu Desktop 24. This can be mounted directly using most virtual machine software. If you are installing to a physical device you can use a tool like [Rufus]() to flash a USB drive with the image to create installation media.

>[!note] Disable Unattended Installation
>Unless you specifically want it, you should disable "unattended installation" in your virtual machine software or boot media imager.

If you have successfully booted the image, you should be greeted by GNU GRUB loader:
![[_Assets/Ubuntu Linux/firstboot.png]]
Selecting "Try or Install Ubuntu" (or letting it auto-select) will load the graphical Ubuntu installer:
![[installer.png]]
The installer GUI is easier to understand than anything I could write. In this guide I will be choosing the following options, but you should determine your own needs:

| **Language**                | English                                                                                       |
| --------------------------- | --------------------------------------------------------------------------------------------- |
| **Accessibility Options**   | None                                                                                          |
| **Keyboard Layout**         | English (US)                                                                                  |
| **Internet Connection**     | Use wired connection<br>(You may want to choose Wi-Fi if you are installing on a real device) |
| **Installation Type**       | Interactive installation                                                                      |
| **Applications**            | Default selection                                                                             |
| **3rd Party Optimizations** | Both                                                                                          |
| **Disk Setup**              | Erase disk and install Ubuntu, no advanced features                                           |
| **Account**                 | Password required: Yes<br>Use Active Directory: No                                            |
Now you may review your choices and install!

You can view installation output details by clicking on the console icon in the bottom right corner:
![[installer-2.PNG]]
Depending on your selections and internet connection this process might take a while as hundreds of MB of packages are downloaded. When it is complete, you will be prompted to restart. Remember to remove your installation media!

With the next boot, you should be able to log in with the account you created during setup.

You have now set up an Ubuntu Linux machine!

# Software Recommendations

Now would be a great time to open the terminal and install the .NET SDK:

```bash
sudo apt update && sudo apt install dotnet-sdk-8.0
```

And for good measure, create a new console application and run it:
```bash
# Make a new directory for the project and navigate to it
mkdir TestProject
cd TestProject

# Create a new project with the 'console' template
dotnet new console

# Run the project
dotnet run
```

It appears there are plenty of .NET project IDE options for Ubuntu via the built-in App Center, such as VS Code and JetBrains Rider.