# Creating your own custom speech ROMs 

## Step 1 – create the list of words/phrases

I started with a plain text file and using Notepad++ on Win10 I created my voice list which looked like this:
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

## Step 2 – pad out the text file

