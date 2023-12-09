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

![RunCPM Folder LayoutYellow boxes](https://github.com/MarkD833/Digitalker-Digital-Voice-Selection-Software/images/YellowBoxes.JPG)

I've recently built an Arduino shield for my Digitialker chip which has been stored in its box for 25+ years! My incentive to create the shield was given a boost by the discovery of quite a few ROM dumps of various pre-configured ROM vocabularies uploaded to the [Internet Archive](https://archive.org/details/digitalker).

This was give a further boost by the recent appearance of a National Semiconductor software product called the Digitalker Vocabulary Selection Software (DTSW-500) on the [bitsavers website](http://bitsavers.informatik.uni-stuttgart.de/components/national/digitalker/NSC_DIGITALKER_CPM/).

From the first paragraph of the DVSS datasheet:
> The DIGITALKER Vocabulary Development System (DVSS) is a CP/M software package which provides 500 highly intelligible English words in a male speaking voice. These words are intended for users of National Semiconductor's DIGITALKER MM54104 Speech Processor Chip. The package provides a complete software environment that allows users to create speech PROMs containinag a vocabulary of words, phrases, or sentences put together from the 500 words supplied.

I already have a small CP/M system based around a few boards from [Small Computer Central](https://smallcomputercentral.com/) so I thought I'd try and see if I could get the DVSS software to work. The user manual for the software isn't included on the disks so presumably was a hard copy distributed with the original software.

After a bit of experimentation, I figured it all out and decided to write it up here for the benefit of others.

The good news is that no actual hardware CP/M system is required in order to use the DVSS programs.

What follows is based on the notes I made at the time - enjoy!

# Access to a CP/M system

I started my DVSS experimenting on my RC2014 CP/M system but then decided to look for a CP/M emulation that would allow experimenting without the need for any CP/M hardware.

After a short search, I came across [RunCPM](https://github.com/MockbaTheBorg/RunCPM). You can read my walkthrough guide here on how I set the CP/M emulator on my Windows 10 PC.
