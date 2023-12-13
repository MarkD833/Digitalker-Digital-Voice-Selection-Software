# Guide to using the National Semiconductor Digitalker Vocabulary Selection Software (DVSS)

## Background

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

After a short search, I came across [RunCPM](https://github.com/MockbaTheBorg/RunCPM). You can read my [walkthrough guide](/RunCPM_Setup.md) on how I set the CP/M emulator on a Windows 10 PC.

# A basic tour of the DVSS programs and files

This section can be skipped as it's just a basic tour of the files and what I think they are/do.

Once I had my CP/M emulator setup with the DVSS software, I had a browse around the files and [documented what I found](/Basic_tour.md) and my thoughts as I explored.

# The VERIFY.VOC file

The VERIFY.VOC (VOC = vocabulary) file is used to specify the words, phrases and sounds that the user wants to include in the final ROMs.

I've [documented what I've discovered](https://github.com/MarkD833/Digitalker-Digital-Voice-Selection-Software/blob/main/Verify.md) about this file as it is the key to creating a custom ROM set.

# A walkthrough creating a custom speech ROM

After playing with the DVSS programs I've figured out how to create custom speech ROMs for the Digitalker chip. I've created a sample [walkthough](/CustomROM.md) that hopefully should allow others to create custom ROMs too. Note that the custom ROMs are limited to using the words and sounds supplied with the original DVSS package.

# A set of ROMs with all the words in the the DVSS library

I've created a set of 5x 16Kbyte ROMs that hold all the words and sounds that are supplied with DVSS. Look for them in the [ROMs](/ROMs) folder.
 
Have fun!
