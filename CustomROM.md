# Creating your own custom speech ROMs 

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
Note the blank line between each entry in the file.

I wanted to know if there was a difference between the sound for a numerical digit (i.e. 1, 2, 3 etc) and the word equivalent (i.e. one, two, three etc). I also wanted to have a quick play with the word endings (entries 11 to 14) and have a go at my first phrase.

## Step 2 – Pad out the text file

This seems to be a CP/M requirement. The text files I've come across so far have all been padded out at the end of the file with ASCII character 27 (0x1A) - appears as SUB in Notepad++ - so that the overall file length is a multiple of 128 bytes.

When using Notepad++, there is a count of the number of bytes in the file displayed in the status bar at the bottom of the screen. For my test file it says 273, so I need to pad the file to 384 bytes (3 x 128).

In order to pad the file out to 384 bytes, I placed the cursor on the line below the 15: and then held down the = key to repeatedly insert the = symbol whilst watching the reported length of the file, stopping when it reached 384.

The end of my file then looked like this:

![Notepad_pp](/images/Npp.png)

Then
* highlight all the = that are at the end of the file
* select Search->Replace from the menu (or Ctrl+H)
* Set "Find what" to the = character
* Set "Replace with" to \x1A

Set the rest of the settings in the dialog box like this:

![Notepad_pp Replace](/images/Npp_Replace.png)

Then click "Replace All". The end of the file then looks like this:

![Notepad_pp Replaced](/images/Npp_Replaced.png)
