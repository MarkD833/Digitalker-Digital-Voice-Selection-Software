# The VERIFY.* demonstration files 

The program disk archive contains 4 files - the .ROM, .SUB, .VOC and .WRK as part of an example ROM setup.

The starting point is the .VOC file. It is processed by the vocabulary list compiler (VLC) and generates the .WRK file.

The .WRK file is then used by the Digitalker I ROM image builder (IBUILD) to creare the .ROM file.

The .ROM file is the file that is programmed into a PROM.

The .SUB file is a batch file that automates the process and is used by the CP/M SUBMIT.COM batch processing command.

## The VERIFY.VOC file format

The VERIFY.VOC file is a plain text file that holds the words and phrases that are going to be built into a ROM.

Here’s the contents of the VERIFY.VOC file from the DVSS archive:
```
#
# This is a test vocabulary used to verify DVSS
#

0: welcome sil40 2 sil80 d sil20 v sil20 s sil20 s

1: enter sil40 1 sil20 million sil40 dollar -s.ms1

2: warning sil640 danger.fue sil160 evacuate sil160 \
	extreme sil40 failure

3: get sil40 ready sil40 4 sil40 a sil40 1 sil40 \
	nano-.rp second sil40 delay.r

4: get sil40 out sil40 of sil40 the.r sil20 rain

10: spell sil40 the.r sil40 word sil320 wednesday

12: that.r sil40 is.r sil40 correct
```
I programmed the VERIFY.ROM file into my flash chip on my Digitalker board. 

When I instruct Digitalker to say word/phrase 0, it speaks “WELCOME TO D V S S”.

For word/phrase 1, it speaks “ENTER 1 MILLION DOLLARS”.

For word/phrase 2, it speaks “WARNING DANGER EVACUATE EXTREME FAILURE”.

For word/phrase 3, it speaks “GET READY FOR A ONE NANO SECOND DELAY”.

For word/phrase 4, it speaks “GET OUT OF THE RAIN”.

For word/phrase 10, it speaks “SPELL THE WORD WEDNESDAY”.

For word/phrase 12, it speaks “THAT IS CORRECT”.

## The format of VERIFY.VOC

This is what I’ve discovered so far about the format of the VERIFY.VOC file.

A line starting with a # is a comment line and is ignored.

A line ending with a \ indicates a continuation on the next line.

Each line ends with a CR (ASCII code 13) and an LF (ASCII code 10).

There is a blank line between each entry in the file consisting of just a CR and an LF. I don’t know if this is purely cosmetic or a requirement at the moment.

A new ROM word (or phrase) starts with a number and a colon. The number is the same number that you pass to the Digitalker chip when selecting what to speak.

Each number must always be larger than the previous number and the numbers don’t have to be sequential as you can see from the VERIFY.VOC file.
 
After the colon there is a space and then the name of the sound in the archive file STDARC.DAT. This is the name as reported by the ALIST command. I don’t know if this is case sensitive or not so probably best to just stick with lower case.

If you wanted word 0 in your ROM to be the word “busy”, then the line would look like this:
```
0: busy
```
If you wanted word 5 in your ROM to be the phrase “going up”, then there are 3 parts to it – the word “going”, a pause and the word “up”.

The entries called sil<xxx> would appear to be periods of silence to be used between words. The number would appear to be the length of the silent period in milliseconds.

To add the phrase “going up” as word 5 in your ROM, then the line would look like this:
```
5: going sil40 up
```
You should experiment with the various periods of silence to see which makes your phrase sound better.

The first few sounds in the vocabulary archive appear to be word endings. Looking at the example ROM, the word “dollar” is made into “dollars” by speaking the –s.ms1 sound immediately after the word.

I’ve not had a chance to discover the difference between –s.ms1 and –s.ms2 yet.

There are also word endings to convert words like “lock” into “locked” and “close” into “closing”. 

There are other words in the vocabulary that have suffixes such as .m, .r, .s, .mt and .p. I don’t know what these signify – perhaps a linguist may know the answer to that.

Then there are what appear to be duplicate words such as wait and wait.r as well as waiting and waiting.s. I need to build a ROM with these words in it to see what audio differences there are.

Note that the text file does need to be padded with the ASCII character 27 (0x1A) so that the file is multiples of 128 bytes long. This seems to be related to CP/M and how it handles file buffers.

If you run the VLC command on an unpadded file, then it causes VLC to report errors. 

