# Creating your own custom Digitalker speech ROMs 

## Step 1 – Create the list of words/phrases

I started with a plain text file and using [Notepad++](https://notepad-plus-plus.org/) on Windows 10 I created my voice list which looked like this:
```
#
# This is a test vocabulary
#

0: zero

1: one

2: two

3: three

4: four

5: five

6: 1

7: 2

8: 3

9: 4

10: 5

11: close

12: close -ing.fs1

13: close -ing.fs2

14: close -ing.ms3

15: the.r sil40 customer sil40 is.r sil40 correct
```
Note the blank line between each entry in the file. I've discovered that this isn't necessary but it makes for easier reading of the file.

The words you would like to use must be spelt as they are in the vocabulary list produced by the ALIST command.
 
I wanted to know if there was a difference between the sound for a numerical digit (i.e. 1, 2, 3 etc) and the word equivalent (i.e. one, two, three etc). I also wanted to have a quick play with the word endings (entries 11 to 14) and have a go at my first phrase.

## Step 2 – Pad out the text file

This seems to be a CP/M requirement. The text files I've come across so far have all been padded out at the end of the file with ASCII character 27 (0x1A) - appears as SUB in Notepad++ - so that the overall file length is a multiple of 128 bytes.

However, I've discovered that if my files are terminated with 128x the 0x1A (SUB) ASCII character, then the DVSS programs don't complain.
 
When using Notepad++, I can put 128 of the # character at the end of the file, highlight all the # characters and use the Replace command to replace them with the character \x1A.

Save the file in the \B\0 folder (assuming you are using the RunCPM emulator). Let's assume you called it TEST1.VOC.

## Step 3 - Compile the list of vocabulary words

Run the RunCPM emulator and switch to the B drive by typing B:<enter> at the prompt. Check that you are in the right place by typing dir<enter> to get a listing of the files.

You should see the various DVSS files and your TEST.VOC file.

Now compile the list of words using the vocabulary list compiler (VLC) like this:

> vlc test1.voc stdarc test1.wrk

That should cause the vocabulary list compiler to generate the work file and output the details of each message. With my test file, the output looks like this:
```
DVSS  <vlc>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Initializing...

Compiling vocabulary list...

Using vocabulary list: <TEST1.VOC>
Using archive: <STDARC>


Message <  0>
   Word   Name
     1    <zero>

Message <  1>
   Word   Name
     1    <one>

Message <  2>
   Word   Name
     1    <two>

Message <  3>
   Word   Name
     1    <three>

Message <  4>
   Word   Name
     1    <four>

Message <  5>
   Word   Name
     1    <five>

Message <  6>
   Word   Name
     1    <1>

Message <  7>
   Word   Name
     1    <2>

Message <  8>
   Word   Name
     1    <3>

Message <  9>
   Word   Name
     1    <4>

Message < 10>
   Word   Name
     1    <5>

Message < 11>
   Word   Name
     1    <close>

Message < 12>
   Word   Name
     1    <close>
     2    <-ing.fs1>

Message < 13>
   Word   Name
     1    <close>
     2    <-ing.fs2>

Message < 14>
   Word   Name
     1    <close>
     2    <-ing.ms3>

Message < 15>
   Word   Name
     1    <the.r>
     2    <sil40>
     3    <customer>
     4    <sil40>
     5    <is.r>
     6    <sil40>
     7    <correct>

Workfile created: <TEST1.WRK>
        Messages: <16>
           Words: <25>

Run complete
```
The number of messages reported should equal the number of messages you've defined in your vocabulary file. If VLC cannot find the word you have types, then it will report that there is a missing word.

## Step 4 - Building the ROM(s)

If all goes well, you are now ready to build the actual ROM(s).

Still on the CPM emulator, type the following:

> ibuild test1.wrk test1.rom

That should cause the IBUILD program to create the binary ROM file(s). With my test file, the output looks like this:
```
DVSS  <ibuild>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Building ROM image...

Workfile <TEST1.WRK> contains 16 message(s)

Message <  0>
   Word   Instructions
     1          7

Message <  1>
   Word   Instructions
     1          4

Message <  2>
   Word   Instructions
     1          7

Message <  3>
   Word   Instructions
     1          4

Message <  4>
   Word   Instructions
     1          6

Message <  5>
   Word   Instructions
     1          4

Message <  6>
   Word   Instructions
     1          4

Message <  7>
   Word   Instructions
     1          7

Message <  8>
   Word   Instructions
     1          4

Message <  9>
   Word   Instructions
     1          6

Message < 10>
   Word   Instructions
     1          4

Message < 11>
   Word   Instructions
     1          8

Message < 12>
   Word   Instructions
     1          8
     2          4

Message < 13>
   Word   Instructions
     1          8
     2          2

Message < 14>
   Word   Instructions
     1          8
     2          1

Message < 15>
   Word   Instructions
     1          5
     2          1
     3         11
     4          1
     5          5
     6          1
     7          8

Writing ROM image to file: <TEST1.ROM>


  Message pointers:    16 (32 bytes)
      Instructions:   129 (387 bytes)
  Speech data used:  2262 bytes
Speech data reused:  3376 bytes

  Total bytes used:  2681 (16%)
  Total bytes left: 13703 (84%)

Run complete
```
From the output of IBUILD, you can see that your chosen vocabulary takes up 2681 bytes leaving 13703 bytes free in the 16K ROM.

I don't recommend using the '-t' command line option with IBUILD as it doesn't report the bytes used.

## Step 5 - Testing the ROM

The TEST1.ROM file should now be visible in the \B\0 folder when viewed using Windows 10 file explorer. You should program this file into your chosen chip - FLASH or EEPROM or EPROM etc - and install the chip in your Digitalker board.

You should now be able to instruct your Digitalker chip to speak each message by referring to the number associated with it in the original TEST.VOC file.

Referring to my test messages file:
* If I tell the Digitalker chip to play back messages 0, 1, 2, 3, 4 and 5 then it says the words zero, one, two, three, four and five.
* If I tell the Digitalker chip to play back messages 6, 7, 8, 9 and 10 then it says the words one, two, three, four and five again.

Constructing a custom message ROM with either the numbers 1, 2, 3 etc generates the same audio output as using the words one, two, three etc.

* Playing back word 11 results in the word “close” and playing back words 12, 13 and 14 results in 3 variations of trying to say the word “closing”.
* Playing back word 15 results in the phrase “THE CUSTOMER IS CORRECT” being spoken.

There’s obviously some tweaking to be done to discover more about the various word endings etc, but that’s my walkthrough for creating a custom ROM.

NOTE: Because of the way the ROM is built, some ROMs will contain more words (or phrases) than others. It seems to be down to the way that parts of the speech data can be reused within the ROM. The more speech data that can be reused, then the more words the ROM can hold.

