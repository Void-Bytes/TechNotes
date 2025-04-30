This page contains tips for the general configuration of Alpine Linux.
# Getting Started

**Introduction to APK, OpenRC, doas**
https://www.youtube.com/watch?v=EaCCB3y1ZGM

# **Software Recommendations**

## Command Line Interface (CLI)

> [!info] These programs are usable via command line.

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

___
## Desktop Environment (XFCE)

>[!info] These programs require a desktop environment to use.

___
### mousepad
Lightweight GUI-based text editor designed for the XFCE desktop environment.

#### Installation
```
doas apk add mousepad
```

**Example Usage**
*Mousepad can be started from a GUI application launcher, or via command line*
```
mousepad my_file.txt
```
___

