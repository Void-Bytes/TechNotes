This page contains tips for the general configuration of Alpine Linux.
# Getting Started
## Requirements
- todo
## Helpful Online Resources
- YouTube Video: **[Introduction to APK, OpenRC, doas](https://www.youtube.com/watch?v=EaCCB3y1ZGM)**
# Setup
This section describes how to set up Alpine Linux once the installation media has been created. Your first should look something like this:
![[firstboot.PNG]]
## Step 1 - Log in as root
Conveniently, on first boot the default username is "root" and there is no password.
Once you have logged in you should be welcomed by the "message of the day":
```
Welcome to Alpine!

The Alpine Wiki contains a large amount of how-to guides and general
information about administrating Alpine systems.
See <https://wiki.alpinelinux.org/>.

You can setup the system with the command: setup-alpine

You may change this message by editing /etc/motd.

localhost:~#
```
## Step 2 - Run setup-alpine
``setup-alpine`` is a prompt-based installation and configuration wizard. It will prompt with questions and options regarding localization, network connectivity, package manager repositories, and user account security. Most of the choices are simple enough that reading the prompts will be sufficient to continue, and often a default option will be provided.

In this guide, I'll be choosing the options I would normally use. It is possible that if you deviate from the guide you will be presented with options not mentioned here.
### Step 2.1 - Hostname
This is the name your device will use to identify itself in networking solutions.
Default is "localhost", but I prefer to set something that identifies the device itself.
For this example I will choose "alpine".
### Step 2.2 - Interface
You will be prompted to configure the available network interface devices.
The default option should be the first interface, if there is one. Setting up Wi-Fi requires an extra step, so that is what I will choose in this tutorial, by entering option "wlan0".

Upon selecting a wireless interface, it will scan for available networks for you to select by typing in  the name of the network, or the associated number in the list. Once you select a network to join, you will be prompted to enter a password if one is required.

Once you have entered the network password you will be prompted to enter your local IP address or let the DHCP server choose one for you. I would recommend letting the DHCP server choose, as it is the easiest and default option.

At this point you may be prompted to configure another interface, if there is one. You likely only need to configure one and can enter "done" to continue. You asked whether you want to do any manual network configuration, to which we say "n".
### Step 2.3 - Root Password
You will be prompted to change the root password. A very strong password is recommended for serious applications, and disabling the root account altogether is recommended for professional applications. For students and hobbyists, short passwords are also permitted for quick login.
### Step 2.4 - Timezone
The next step is to select your time zone. If you know your time zone ID, you can type it in directly, otherwise you can search for it by first typing in the primary time zone given by the wizard, or by selecting a sub-time zone. I would usually enter "America/Phoenix", but someone living in California might enter "PST8PDT"
### Step 2.5 - Proxy
I don't usually take advantage of this option, but it is available. Press enter to continue with "none".
### Step 2.6 - Network Time Protocol
Select which time-keeping service to use in your system. I usually go with the default, "chrony".
### Step 2.7 - APK Mirror
In this step you select which mirror of the Alpine Package Keeper repositories you want to use. A tool is provided to scan for the fastest mirror available. I usually just press "1" to choose the official mirror, after enabling the Community Repository of course.

>[!info]
>You can enable the Community repository here by entering "c". You will still be allowed to choose a mirror after toggling that option.
>
>I would recommend enabling the Community repository if you are just messing around, as it houses a lot of interesting packages to install with ``apk``
### Step 2.8 - User
In this step you are prompted to set up a user account by entering their username.

>[!warning]
>This step is optional for command line interactions, but
>***you must set up a user account if you intend to install a desktop environment like XFCE***.

After entering a username, you are prompted to give the account a full name, or label, and set its login password. This account will have super-user privileges, and so the password philosophy described in Step 2.3 applies here as well.

You will also be prompted about providing an existing SSH key and selecting an SSH server type. I would recommend leaving these default unless you happen to have a specific type of SSH key and want to use it now.
### Step 2.9 - Disk & Install
Things might vary by hardware configuration here. On a typical computer it might list the currently attached disks by ID along with some information to help distinguish them from each other. The default option is "none" for if you don't want to do a permanent installation of the system.

In the simplest case, your option might be something like "sda" for a hard drive.

>[!info] Raspberry Pi - SD Card Install
If you are using a [[Raspberry Pi]], you might be notified that there are no disks available, and asked if you want to try boot media. At this you should enter "y". It should then list something like "mmcblk0" which is the SD card in the Pi. Remember to type it in because the default option is "none".

Once a disk is selected, we choose the type of installation. In this guide we will be doing a "sys" or System installation, as a normal permanent installation to disk. You will be given one final chance to confirm your selections, and with a "y" the installation will begin.

On modern hardware the installation should go incredibly quickly, and when it is completed a message should be printed:
```
Installation is complete. Please reboot.
```

And to reboot, simply enter the command "reboot". When the system restarts your configuration should be saved, and you should now be able to log in as your user account and begin installing useful packages.

>[!info] Remove Installation Media
>Remember to remove the installation media so that you boot from the system installation.
# Important Commands

## doas
Executes a command as super-user with root privileges. Similar to "sudo" in other Linux distributions.
```
doas [command]
```
## Power Control Commands
By default, the power control commands are restricted to super-user access. If you are logged in as root it would not be necessary to prefix with ``doas``.
### Power Off
```
doas poweroff
```
### Reboot
```
doas reboot
```

# **Software Recommendations**
This section contains a list of broadly useful software packages and includes installation instructions and example usages of each.

>[!warning] Some of these packages may require the "community" repository to be enabled.

## Command Line Interface Programs

> [!info] These programs are primarily usable via command line interface (CLI).

___
### git
Facilitates file version and management, as well as synchronization with remote code repositories.
#### Installation
```
doas apk add git
```
#### Examples
*Clones the AlpiDotNet repository from GitHub to the current directory*
```
git clone https://github.com/Braveskin/AlpiDotNet
```
___
### dotnet8-sdk
Facilitates building and running .NET and ASP.NET applications on-device.
### Installation
```
doas apk add dotnet8-sdk
```
#### Examples
*Creates a new C# .NET console application project template in the current directory*
```
dotnet new console
```
*Builds and runs the .NET project in the current directory*
```
dotnet run
```
___
### gcc
Facilitates compiling C/C++ programs into executable binaries.
#### Installation
```
doas apk add gcc
```
#### Examples
##### **Step 1** - Write a C program
Use a preferred text editor to create a valid C program file:

**hello_world.c**
```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```
##### **Step 2** - Compile the program
*Compiles the code file 'hello_world.c' and output it as an executable called 'hello_world'*
```
gcc hello_world.c -o hello_world
```
##### **Step 3** - Run the program
*Runs the compiled program called 'hello_world'*
```
./hello_world
```
Example output:
```
alpine:~$ ./hello_world
Hello, World!
alpine:~$ 
```
___
### make
Facilitates scripting C/C++ compilation to include environment variables, build event functions, and configuring source and output controls.
#### Installation
```
doas apk add make
```
#### Examples
##### **Step 1** - Create a makefile
``make`` reads a file called "makefile" for instructions. The example below directs ``make`` to read all ".c" files from the "src" directory, store compilation objects in "obj", and output the compiled binary in "bin".

**makefile**
```bash
EXE_NAME = hello_world

SRC_DIR = ./src
OBJ_DIR = ./obj
BIN_DIR = ./bin

DEBUG = -O3
INCLUDE = -I/usr/local/include
CFLAGS = $(DEBUG) $(INCLUDE) $(EXTRA_CFLAGS)

LDFLAGS = -L/usr/local/lib

SOURCES := $(notdir $(wildcard $(SRC_DIR)/*.c))
OBJECTS := $(SOURCES:%.c=$(OBJ_DIR)/%.o)

all: $(BIN_DIR)/$(EXE_NAME)

$(BIN_DIR)/$(EXE_NAME): $(OBJECTS)
	mkdir -p $(BIN_DIR)
	$(CC) $(LDFLAGS) -o $@ $^

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
	mkdir -p $(OBJ_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -rf $(BIN_DIR) $(OBJ_DIR)
```

Note in this example the first line is a variable that allows you to set the name of the output executable. In this example we will use the same script as the ``gcc`` example.
##### **Step 2** - Add source files
Create a new source file in a directory "src", or move the script from the ``gcc`` example there:
```bash
mv hello_world.c src/hello_world.c
```
When your source files are placed, your project ``tree`` should look something like this:
```bash
.
├── makefile
└── src
    └── hello_world.cs

1 directories, 2 files
```
#### **Step 3** - Run make
Running make will build the executable using the source files.
```
make
```
After a successful ``make``, your ``tree`` should look something like this:
```
.
├── bin
│   └── hello_world
├── makefile
├── obj
│   └── hello_world.o
└── src
    └── hello_world.c

3 directories, 4 files
```
##### **Step 4** - Run the program
The compiled program can be run the same was as in the ``gcc`` example, except the executable was output to the "bin" directory:
```
./bin/hello_world
```
##### **Step 5** - Clean the project directory (Optional)
The makefile above also includes a "clean" directive that will delete the "bin" and "obj" directories, returning the project directory to its original state before running ``make``, in Step 2.

___
## Desktop Environment (XFCE) Programs

>[!info] These programs require a desktop environment to use.

___
### xfce4-wavelan-plugin
Panel item that displays current Wi-Fi connection status, signal strength and local IP address.
#### Installation
```
doas apk add xfce4-wavelan-plugin
```
#### Examples
##### **Step 1** - Access the "Add New Items" menu for your chosen panel
![[add-panel-item.png]]
##### **Step 2** - Add the "Wavelan" panel item
![[wavelan-search.png]]
##### **Step 3** - Access the Wavelan Plugin Options via the panel item Properties
![[wavelan-context-menu.png]]
##### **Step 4** - Configure the plugin with your preferences
![[wavelan-options.png]]
While using a [[Raspberry Pi]], I always have to switch the Interface from "Io" to "wlan0", and I prefer to turn off the signal bar for cleanliness of appearance.
### xfce4-cpugraph-plugin
Panel item that displays current per-core CPU load and a histogram of average load.
#### Installation
```
doas apk add xfce4-cpugraph-plugin
```
#### Examples
##### **Step 1** - Add the "CPU Graph" panel item
![[cpugraph-search.PNG]]
##### **Step 2** - Configure the graph options
![[cpugraph-options.PNG]]
I usually just increase the update interval to 500ms and increase the width to comfort.

___
### mousepad
Lightweight GUI-based text editor designed for the XFCE desktop environment.
#### Installation
```
doas apk add mousepad
```
#### Examples
*Mousepad can be started from a GUI application launcher, or via command line*
```
mousepad my_file.txt
```
___

