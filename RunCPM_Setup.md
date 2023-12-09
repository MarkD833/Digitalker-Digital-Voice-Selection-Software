# Guide to setting up a CP/M emulator on Windows 10

This file is part of my exploration of the National Semiconductor Digitalker Vocabulary Selection Software (DTSW-500) and details my progress in setting up a CP/M emulator that can be used for exploring and experimenting with the DVSS program suite.

## Background

Once I got the DVSS programs to run on my CP/M system, it became apparent that it was a real pain trying to transfer files between my CP/M system and my Windows 10 PC. This is most likely due to my inexperience with the CP/M OS.

I also wanted to try and make my findings available to more than just people interested in Digitalkler who also happend to have some CP/M hardware.

I started looking for a CP/M emulator to see what options there were. There are a few emulators out there, but the one that caught my eye is called [RunCPM](https://github.com/MockbaTheBorg/RunCPM). The particularly interesting feature that caught my eye was:

> RunCPM emulates the CP/M disks and user areas by means of subfolders under the RunCPM executable location

Hooray, no more transferring files between CP/M and WIndows 10.

## Getting and building RunCPM

Get RunCPM from the link above. RunCPM is supplied as source code that needs building for your particular PC. I have the free version of Visual Studio 2022 and the solution file opened without any problems for me. I then simply built the program without changing any settings.

This results in a RunCPM.exe file being created.

## Setting up RunCPM

Once you have the executable file, there a few simple folders that need setting up.

Start by creating a folder for your RunCPM.exe file. I created D:\RunCPM as mine. I then created a folder called A (upper case) with subfolder inside the A folder called 0 (zero). I also created folders called B & C, each with a subfolder called 0.

My folder layout looks like this:

![RunCPM Folder Layout](https://github.com/MarkD833/Digitalker-Digital-Voice-Selection-Software/blob/main/images/RunCPM_folders.png)

In the zip archive of RunCPM, there is a folder called DISK. Inside that folder there is a zip file called A.ZIP. Unzip all the files into your \A\0 folder.

Your CP/M system is now setup and you can try running it by double clicking on the RunCPM.exe file. If successful, you should have a window like this one appear:

![RunCPM shell](https://github.com/MarkD833/Digitalker-Digital-Voice-Selection-Software/blob/main/images/RunCPM_shell.png)

## Extracting the Digitalker DVSS software from the archive files

Head on over to the [bitsavers website](http://bitsavers.informatik.uni-stuttgart.de/components/national/digitalker/NSC_DIGITALKER_CPM/) and download these 2 files:

> nsc_digitalker_archive_disk.img
> nsc_digitalker_porgam_disk.img  (their spelling, not mine!)

