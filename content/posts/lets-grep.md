---
title: "Lets Grep"
date: 2022-02-16T12:46:29-08:00
---

We've all had to look for text in files. The "manual" way to do that is open the text files, one at a time, in some code editor and do a `cmd-f` or `ctrl-f` and search for the text. Then, once you've found the text, you make a note of it. And you repeat this process for each and every file. Imagine the time and manual effort this would take for hundreds of files.

There's automation tooling available to assist you in accomplishing this!

Meet `grep`. `grep` is a command line tool that is available on Linux and Linux based Operating Systems - such as Mac OS X. `grep` allows you to search for a text string across multiple files. Let's look into how.

## Check if grep exists on your machine

Open up a Terminal on your machine.

```
$ grep
usage: grep [-abcdDEFGHhIiJLlMmnOopqRSsUVvwXxZz] [-A num] [-B num] [-C[num]]
	[-e pattern] [-f file] [--binary-files=value] [--color=when]
	[--context[=num]] [--directories=action] [--label] [--line-buffered]
	[--null] [pattern] [file ...]
```

## Search for a text string in one file

There's sample files to work with - in 'examples/text-files'. Download and copy these files into a directory on your machine. In these examples we'll assume that directory is 'myFiles'.

```
$ cd myFiles
```

```
$ grep 'text' text1.txt
```

The output of the command will list the two lines that contain the word `text`. Note that all the other lines that don't include the word are not outputted.
```
This is a text file.
I like to work with text.
```

If you grep in a file that does not have the word in it, then the output will be empty.

```
$ grep 'text' text3.txt

```

## Search for a text string in multiple files

You can specify multiple files to search through. `grep` will output the matching lines, with the text filename for the matching line included.

```
$ grep 'text' text1.txt text2.txt text3.txt

text1.txt:This is a text file.
text1.txt:I like to work with text.
text2.txt:This is a second text file.
```

## Search for a text string in all files in a directory

If you want to search through all files, but don't want to specify each one, you can search through all files in a directory.

Here, you search through all files in the current directory, where the current directory is specificed by `.`. You'll use the recursive `-R` option flag to specify that you want to search through all files in this directory. You'll get a similar output where the filename and the matching lines of text are outputted.

```
$ grep -R 'text' .

./text1.txt:This is a text file.
./text1.txt:I like to work with text.
./text2.txt:This is a second text file.
```

## Case insensitive

Sometimes, you'll want to find all text matches irregardless of upper or lower case. For that, you'll use the `-i` option flag.

```
$ grep -iR 'text' .

./text1.txt:This is a text file.
./text1.txt:Text is nice.
./text1.txt:I like to work with text.
./text2.txt:This is a second text file.
```

Note the second line output - that is `Text` with an upper case `T`.