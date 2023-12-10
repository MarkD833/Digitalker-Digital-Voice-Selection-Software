# A basic tour of the Digitalker DVSS files

This text documents what I have discovered to date about the DVSS suite.

## The files

There are 6 executable files:
```
ALIST  - list the contents of an archive
CRCK   – checksum calculator
IBUILD - Digitalker I ROM image builder
IBURN  - ROM image programming for the Starplex
VLC    - vocabulary list compiler
VLE    - vocabulary list editor
```
There are 4 "VERIFY" files which are the key:
```
VERIFY.ROM – prebuilt ROM image that can be burnt to FLASH
VERIFY.SUB – a script that builds the ROM image
VERIFY.VOC – source file of words/phrases/sounds to speak
VERIFY.WRK – an intermediate work file
```
There are 2 library files that hold the vocabulary:
```
STDARC.DAT - database of sounds, words, numbers etc
STDARC.IDX - likely the index into the database
```
And there are 2 additional files:
```
CRCKLIST.CRC - this it a list of checksums for the various files
DVSSBT.OVR   - likely some sort of overlay file used by the executables
```

* [ALIST](#ALIST)  - list the contents of an archive
CRCK   – checksum calculator
IBUILD - Digitalker I ROM image builder
IBURN  - ROM image programming for the Starplex
VLC    - vocabulary list compiler
VLE    - vocabulary list editor

## A tour of some of the files in more detail

The DVSS files are on the B drive. Within the CP/M emulator just type B: to change to the B drive.

I found that for most files, typing the name of the file followed by a ? (question mark) caused the program to display some usage information. For each of the programs I tried on the CP/M emulator, I've shown the output generated.

---
### ALIST

The ALIST.COM program lists the contents of a vocabulary archive.

Typing ALIST ? results in the following:
```
DVSS  <alist>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Name:
        alist -- list the contents of an archive
Usage:
        alist [-ln] [-p] [-t] archive [file]
Options:
        '-ln' -- "n" is the listing page length (default=66)
        '-p' -- send output to printer
        '-t' -- terse mode (suppress informational messages)
Arguments:
        'archive' -- the name of the archive to list
        'file' -- the name of the output file to create
```
I then made a guess and typed:
```
alist stdarc
```
This caused the ALIST program to dump out the contents of the STDARC archive. You can see the output of 600+ vocabulary entries [here](https://github.com/MarkD833/Digitalker-Digital-Voice-Selection-Software/blob/main/Vocabulary.md).

---
### CRCK.COM – CRC calculation

Typing CRCK ? didn't provide any useful hints, but omitting the ? did:
```
++NO FILE NAME SPECIFIED++

To use this program:

        COMMANDS:   CRCK [drive:]<filename.filetype> [F]

        Examples:

                CRCK MYFILE.ASM Check only MYFILE.ASM

                CRCK *.ASM      Check all .ASM files

                CRCK *.* F      Check all files and make file
                                of results <CRCKLIST.CRC>
```
Performing a CRC check on the ALIST.COM file results in the following output:
```
CRCK ver 4.3 - 24K Buffer - 01/17/81 RBS
CTL-S pauses, CTL-C aborts

ALIST   .COM    CRC = 4F D0

DONE
```
The value (checksum) reported is the same as that detailed in the CRCLIST.CRC file in the program archive.

---
### IBUILD.COM – Digitalker I ROM image builder

Typing IBUILD ? results in the following:
```
DVSS  <ibuild>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Name:
        ibuild -- Digitalker I ROM image builder
Usage:
        ibuild [-p] [-v] workfile romfile
Options:
        '-p' -- send output to console and printer
        '-t' -- terse mode (suppress informational messages)
Arguments:
        'workfile' -- the name of an existing workfile
        'romfile' -- the name of the ROM image file to create
```
If I use the work file supplied with DVSS and I run IBUILD with the command:
```
ibuild verify.wrk test.rom
```
Then I get the following output:
```
DVSS  <ibuild>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Building ROM image...

Workfile <VERIFY.WRK> contains 13 message(s)

Message <  0>
   Word   Instructions
     1          9
     2          1
     3          7
     4          1
     5          5
     6          1
     7          6
     8          1
     9          7
    10          1
    11          7

Message <  1>
   Word   Instructions
     1          5
     2          1
     3          4
     4          1
     5          6
     6          1
     7          5
     8          4

Message <  2>
   Word   Instructions
     1          7
     2          2
     3          9
     4          1
     5          9
     6          1
     7         18
     8          1
     9          5

Message <  3>
   Word   Instructions
     1          9
     2          1
     3          6
     4          1
     5          6
     6          1
     7          3
     8          1
     9          4
    10          1
    11          3
    12         17
    13          1
    14          3

Message <  4>
   Word   Instructions
     1          9
     2          1
     3          6
     4          1
     5          4
     6          1
     7          5
     8          1
     9          3

Message < 10>
   Word   Instructions
     1         13
     2          1
     3          5
     4          1
     5          8
     6          1
     7         10

Message < 12>
   Word   Instructions
     1          5
     2          1
     3          5
     4          1
     5          8

Writing ROM image to file: <TEST.ROM>


  Message pointers:    13 (26 bytes)
      Instructions:   274 (822 bytes)
  Speech data used:  4523 bytes
Speech data reused:  3758 bytes

  Total bytes used:  5371 (33%)
  Total bytes left: 11013 (67%)

Run complete
```
The byte count at the end of the process looks useful in determining when the ROMs are getting full.

It also looks like the IBUILD program is working with a pair of ROMs to give a total capacity of 16Kbytes.

---
### IBURN.COM – ROM image programming for the Starplex 

Typing IBURN ? results in the following:
```
DVSS  <iburn>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Name:
        iburn -- ROM image programming for the Starplex
Usage:
        iburn imagefile promtype
Arguments:
        'imagefile' -- the name of an existing ROM image file
        'promtype' -- type of PROM to program (2716 or 2732)
```
“Starplex” was a National Semiconductor development system that appeared to include a PROM programmer functionality.

I think this program can be ignored as the created ROMs will now be burnt using a modern PROM programmer.

---
### VLC.COM – Vocabulary list compiler

Typing VLC ? results in the following:
```
DVSS  <vlc>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Name:
        vlc -- vocabulary list compiler
Usage:
        vlc [-c] [-p] [-t] vocab archive workfile
Options:
        '-c' -- check mode (suppress workfile creation)
        '-p' -- send output to console and printer
        '-t' -- terse mode (suppress informational messages)
Arguments:
        'vocab' -- the name of an existing vocabulary list
        'archive' -- the name of an existing archive
        'workfile' -- the name of the workfile to create
```
If I run VLC using the supplied VERIFY.VOC file with the command:
```
vlc verify.voc stdarc test.wrk
```
Then I get the following output:
```
DVSS  <vlc>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Initializing...

Compiling vocabulary list...

Using vocabulary list: <VERIFY.VOC>
Using archive: <C:STDARC>


Message <  0>
   Word   Name
     1    <welcome>
     2    <sil40>
     3    <2>
     4    <sil80>
     5    <d>
     6    <sil20>
     7    <v>
     8    <sil20>
     9    <s>
    10    <sil20>
    11    <s>

Message <  1>
   Word   Name
     1    <enter>
     2    <sil40>
     3    <1>
     4    <sil20>
     5    <million>
     6    <sil40>
     7    <dollar>
     8    <-s.ms1>

Message <  2>
   Word   Name
     1    <warning>
     2    <sil640>
     3    <danger.fue>
     4    <sil160>
     5    <evacuate>
     6    <sil160>
     7    <extreme>
     8    <sil40>
     9    <failure>

Message <  3>
   Word   Name
     1    <get>
     2    <sil40>
     3    <ready>
     4    <sil40>
     5    <4>
     6    <sil40>
     7    <a>
     8    <sil40>
     9    <1>
    10    <sil40>
    11    <nano-.rp>
    12    <second>
    13    <sil40>
    14    <delay.r>

Message <  4>
   Word   Name
     1    <get>
     2    <sil40>
     3    <out>
     4    <sil40>
     5    <of>
     6    <sil40>
     7    <the.r>
     8    <sil20>
     9    <rain>

Message < 10>
   Word   Name
     1    <spell>
     2    <sil40>
     3    <the.r>
     4    <sil40>
     5    <word>
     6    <sil320>
     7    <wednesday>

Message < 12>
   Word   Name
     1    <that.r>
     2    <sil40>
     3    <is.r>
     4    <sil40>
     5    <correct>

Workfile created: <TEST.WRK>
        Messages: <13>
           Words: <63>

Run complete
```
VLC seems to be ok with the sample file supplied and doesn’t report any errors.

---
### VLE.COM – Vocabulary list editor

Typing VLE ? results in the following:
```
DVSS  <vle>  v1.0
Copyright (C) 1983
National Semiconductor Corporation

Name:
        vle -- vocabulary list editor
Usage:
        vle [-t] [file]
Options:
        '-t' -- terse mode (suppress informational messages) 
Arguments:
        'file' -- the name of a new or existing vocabulary list
```
I assume that this is some sort of text editor that the end user would use to create the required vocabulary file.

There are no clues as to what the actual commands are once the editor is running and an examination of the binary file in HxD did not reveal any further clues.

If its purpose is to create the .voc file for the vocabulary list compiler, then I think VLE can be ignored and a simple plain text editor on the PC would suffice.

---
### CRCLIST.CRC

Viewing this file in Notepad++ (and HxD) indicates that it is an ASCII text file that seems to be padded at the end, to make the file a multiple of 128 bytes long, with the ASCII character 27 (0x1A) => SUB which appears to equate to CTRL+Z.

For the program disk it contains:
```
VLE     .COM	CRC = 57 F2
VLC     .COM	CRC = 14 B8
IBUILD  .COM	CRC = FE 22
IBURN   .COM	CRC = 5C 54
ALIST   .COM	CRC = 4F D0
VERIFY  .VOC	CRC = 63 FB
VERIFY  .WRK	CRC = BF F3
VERIFY  .ROM	CRC = D2 03
DVSSBT  .OVR	CRC = 4C 99
```
For the archive disk it contains:
```
STDARC  .IDX	CRC = 4E 43
STDARC  .DAT	CRC = 89 94
```
These files are generated by the CRCK.COM program.
