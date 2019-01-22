---
title: Intro to Bash Shell
date: Jan. 22, 2019
author: Tim Dennis
---

# UCLA Data Science Center - Intro to Shell

## Before class:

- set up shell:

  - `exec bash` - switches to bash from zsh
  - enlarge text size - via preferences
  - `export PS1='$ '`
  - `export PROMPT_COMMAND="history 1 >> ~/Dropbox/UnixHistory.txt"`
  - Turn off the text coloring in terminal (`Terminal -> Preferences -> ANSI`)

- students check software installation: Unix, git (with XCode)

- Get the etherpad link
- Have ppl `git clone` if they know `git`

## Checklist for class:

- review of pre-class survey
- mixed audience, both novice/experienced and disciplines
- if material is review for you, help by keeping notes on etherpad and helping your neighbor
- scientific computing has a long history of being self taught, so most instructors even learn something new

## Setup

- Most tasks in the shell can be done with mouse on Desktop. Why do anything differently?
- **Motivation**
- Unix = old school system, created before most in this room were born
- Combining powerful tools together using minimal keystrokes
- Automating repetitive tasks: moving files
- Required to use high performance computing systems, supercomputers, cloud computing
- Terms: file, directory/folder

## Get data
- <http://swcarpentry.github.io/shell-novice/shell-novice-data.zip>, move to Desktop, double click to unzip (if not already done)

## Introducing the Shell

**Objectives:** orient to shell and how it relates to the computer, understand the benefit of CLI

### What computers do:

  1. run programs
  2. store data
  3. communicate with each other
  4. communicate with us → today you'll learn a new way of doing this

### terms:

  - graphical user interface: _GUI_
  - command line interface: _CLI_

### how it works -- the Read Evaluate Print Loop (REPL):

  - you type something - LOOP
  - computer reads it - READ
  - executes command - EVAL
  - prints output - PRINT
  - use **command shell** to make this happen: this is the interface between user and computer

- bash: Bourne again shell, most commonly used, default on most modern implementations

- example data:

  - our friend Nelle has six months worth of survey data collected from the North Pacific
  - 300 samples of **goo**
  - Her pipeline:

    1. Determine the abundance of 300 proteins
    2. Each sample has one output file with one line for each protein
    3. calculate statistics for each protein separately using program `goostat`
    4. compare statistics for proteins using program called `goodiff`
    5. write up results and submit by end of month

  - if she enters all commands by hand, will need to do **45,150 times**.

  - What can she do instead?

- Key terms in Etherpad/Whiteboard

- _Shell_

- _CLI_ & _GUI_

- Benefits of the CLI

  - Automate repetitive tasks (**30 minutes** vs. **2 weeks**)
  - Prevent user error, manual error
  - Processing pipelnes are re-usable and sharable

- _REPL_ Read-Evaluate-Print-Loop

## Files and Directories

**Objectives:** paths, learn basic commands for working with files and directories, learn syntax of commands, tab-completion

- prompt: `$` indicates computer is ready to accept commands

```bash
whoami
```

This command:

1. finds program
2. runs program
3. displays program's output
4. displays new prompt

5. `pwd` print working directory, in this case it is also the home directory

```bash
pwd
```

Look at directory structure image

![Directory structure](http://swcarpentry.github.io/shell-novice/fig/filesystem.svg)

- root directory: holds everything else, begins with slash `/`
- structure of directories: nested
- slashes `\` can also be a separator between names

- `ls` listing, prints names of files and directories in current directory and prints in alphabetical order

```bash
ls
```

- make the output more comprehensible bny using the **flag**`-F`

```bash
ls -F
```

- adds trailing / to names of directories
- spaces and capitalization in commands are important!
- `-F` is an **option, argument, or flag**
- `ls` has lots of other options. Let's find out what they are by:

```bash
ls --help
```

- many bash commands and programs support a `--help` flag to display more information
- for more information on how to usr `ls` type `man ls` (caveat WINDOWS users)
- `man` is for manual and prints the description of a command and options
- Git for Windows doesn't come with the `man` files, instead do a web search for `unix man page COMMAND`
- to navigate `man` files use the up and down arrows, or space bar and b for paging, to quit `q`
- We can also `ls` to see contents of another directory:

```bash
ls -F Desktop
```

- we `ls -F` (??) to the Desktop from out home dir and we see a 'data-shell/' folder
- using a bash shell is strongly dependent on the idea that your files are organized in an hierarchical file system
- why? use
- let's look inside `data-shell`

```bash
ls -F Desktop/data-shell
```

- Let's change directories into that folder

```bash
cd Desktop/data-shell
```

- see where we are:

```bash
pwd
```

```bash
ls -F
```

- we can go down the directory structure, how do we go up?

```bash
cd data-shell
```

- doesn't work, but there are different ways to see directories above your pwd

```bash
cd ..
```

- goes up one level in file hierarchy
- `..` is special directory name meaning "the dir containing this one" (parent)
- can also use absolute paths

```bash
pwd
```

- `ls -F -a` to see hidden files, including `.` and `..`
- `-a` stands for show all
- `.` is for current directory.

```bash
cd
```

- by itself will return you to your `home` directory
- `pwd`
- how do we get back to data

```bash
cd Desktop/data-shell/data
```

- we can string together a list of directories at once
- so far we have been using **relative paths** paths starting from our current directory
- we can also use **absolute paths** in ls and cd, use `pwd`

```bash
cd /Users/nelle/Desktop/data-shell
```

```bash
pwd
```

- two more short cuts: `~` and `-`
- file organization:

  - `ls north-pacific-gyre/2012-07-03/`
  - tab completion

- challenges: open <http://swcarpentry.github.io/shell-novice/02-filedir/#absolute-vs-relative-paths>

- _prompt_

- _pwd_, _ls_, _cd_

- _File systems_

# CREATING THINGS

**Objectives:** create directory hierarchy that matches given diagram, create files, look in folders, delete folders

- go back to the `data-shell` directory (how?) - glad you asked!

```bash
pwd
ls -F
```

- Let's create a directory called `thesis`

```
mkdir thesis
```

- `mkdir` MAKES directories

**good names for directories:**

- is the comment in shell
- don't use whitespaces - whitespaces used to break arguments on CLI, avoid, use `-` or `_` **snail style**
- don't begin with `-`
- commands treat names starting with `-` as options
- stay with letters, numbers , ., - and _
- if you need to refer to names of files or directories that have whitespaces, quote them

```bash
ls -F
```

- nothing there yet
- let's change directory to inside the `thesis` and create a file called `draft.txt`

```bash
nano draft.txt
```

- FOR windows peeps: if you installed the SWC windows installer, it should have installed 'nano', but if not used notepad or notepad++ (NO Word or wordpad)
- NANO
- creates file, opens text editor
- Editors are like cars -- everyone wants to customize them, so there are hundreds if not thousands of different models
- write text
- use `Control+O` to save file shorthand is `^O`)
- `Control+X` to exit
- I don't like this draft, let's remove it:

```bash
ls
rm draft.txt
ls
```

- where does file go? Can i get it back?
- Gone Pecan!
- Deleting is forever!
- recreate file then move up one directory

```bash
nano draft.txt
cd ..
```

- now let's try and remove a directory
- removing a directory:
- `rm thesis`: error
- `rmdir thesis`: still get error
- `rm thesis/draft.txt`
- `rmdir thesis`
- could've also used `rm -r thesis`, but that can be dangerous!

- Let's recreate thesis and draft.

```bash
mkdir thesis
```

```bash
nano thesis/draft.txt
ls thesis
```

- but `draft.txt` isn't very informative, let's rename it using the `mv` command

```bash
mv thesis/draft.txt thesis/quotes.txt
ls thesis
```

- first part of mv is what you want to move, second is to where and including the new name
- **note**: `mv` works on directories as well
- let's move quotes into the current directory: remember the `.`

```bash
mv thesis/quotes.txt .
```

```bash
ls thesis
```

- ls `<filename>` will only list that file, let's see that our file is there

```bash
ls quotes.txt
```

- if we want to keep the old version, we can use copy

```bash
cp quotes.txt thesis/quotations.txt
```

```bash
ls quotes.txt thesis/quotations.txt
```

- let's removed the copied version

```bash
rm quotes.txt
ls quotes.txt thesis/quotations.txt
```

- challenges: open <http://swcarpentry.github.io/shell-novice/03-create/#renaming-files>

- _mkdir_

- _nano_ _(editor)_

- _rm_, _rmdir_

- _mv_, _cp_

## Pipes and Filters

sro **Objectives:** redirect command output to file, construct pipelines

- now we can move around and create things, let's see how we can combine existing programs in new ways
- Let's got into the molecules directory

```bash
ls molecules
```

```bash
cd molecules
```

- the `*.pdb` format indicates these are Protein Data Bank files
- let's use the `wc` command -- stands for word count, but also counts lines and characters

```bash
wc *.pdb
```

- the `*` matches zero or more characters, so the shell turns `*.pdb` into a list of all `.pdb` files
- word count: lines, words, characters
- `*` is a wildcard, it matches anything (zero or more characters, there are others)

**wc and flags**

```bash
wc -l *.pdb
```

- only report number of lines
- what if we do this?

```bash
wc -l *.pdb > lengths.txt
```

- this will send output (redirect it) to new file named lengths.txt
- but let's confirm that it worked by using a new command `cat` - let's us look inside the file, stands for concatenate

```bash
ls lengths.txt
cat lengths.txt
```

- NOtE: `>` will overwrite previous file
- what does `>>` do?
- Try it and run cat
- can't remember how wc reports? use `man wc` (`q` to exit), `wc -h`, or `wc –help` (this should work for most unix commands), also google man wc
- now let's use the `sort` command to sort the contents of our file
- we will use the `-n` flag to tell sort to sort by numerical rather than alpha

```bash
sort -n lengths.txt
```

- sort by first column, using numerical order
- does not change file, just prints output to screen
- if we want to do that use;

```bash
sort -n lengths.txt > sorted-lengths.txt
```

- arrow up to recall last command
- let's use head to see the biggest:

```bash
head -1 sorted-lengths.txt
```

- final result: which one file is shortest?

```bash
sort -n lengths.txt | head -l
```

- **vertical bar** is a pipe, which sends output of command on left as input to command on right
- `head` prints specified number of lines from top of file

```bash
wc -l *.pdb | sort -n | head -1
```

**programming model: pipes and filters**

- note: you only enter the original files once!
- standard input, standard output

## Nelle's pipeline:

- start in her home directory (`users/Nelle`)

```bash
cd north-pacific-gyre/2012-07-03
```

- all files should contain same amount of data
- any files contain too little data?

```
wc -l *.txt | sort -n | head -5
```

- any files contain too much data?

```
wc -l *.txt | sort -n | tail -5
```

- file marked with Z? outside naming convention, may contain missing data

```
ls *Z.txt
```

- records note no depth recorded for these samples
- may not want to remove, but will later select all other files using `[AB].txt`
- Socrative questions 5 and 6

## Loops

**Objectives:** write loops that apply commands to series of files, trace values in loops, explain variables vs values, why spaces and punctuation shouldn't be used in file names, history, executing commands again

- what if you wanted to perform the same commands over and over again on multiple files?
- supposed we have several hundred genome data files named xxx.dat, bbb.dat, etc.
- go to creatures directory `data-shell/creatures`
- may try:

```bash
cp *.dat original-*.dat
```

- but doesn't work. Why?
- really you are saying this:

```bash
cp basilisk.dat unicorn.dat original-*.dat
```

- problem is that when copy receives two files it expects the last one to be a directory in which to copy the files
- you can perform these operations using a loop
- example looking at first three lines in each file

```bash
for filename in basilisk.dat unicorn.dat
  do
    head -3 $filename
  done
```

- what does this look like when you arrow back up?
- explain syntax: filename is variable, what does it stand for? how is it represented later?
- shell prompt changes, if you get stuck, use `control+c` to get out
- can specify whatever variable name you want
- why might it be problematic to have filenames with spaces?
- you can include multiple commands in a loop:

```bash
for filename in *.dat
  do
    echo $filename
    head -100 $filename | tail -20
  done
```

- use of wildcard. what does echo do? why is this useful for loops?
- write a for loop to resolve the original problem of creating a backup (copy of original data)
- strategy: `echo` command before running final, to make sure loop is functioning the way you expect
- going back to the original file copying problem, we can solve:

```bash
for filename in *.dat
do
  cp $filename original-$filename
done
```

- nelle's example:

```bash
cd north-pacific-gyre/2012-07-03
```

- check:

```
for datafile in *[AB].txt; do; echo $datafile; done`
```

- add command:

```
for datafile in *[AB].txt; do; echo $datafile stats-$datafile; done
```

- add command:

```
<!-- for datafile in *[AB].txt; do; goostats $datafile stats-$datafile; done -->
```

- (kill job using ^C)
- add echo:

```
for datafile in *[AB].txt; do; echo $datafile; goostats $datafile stats-$datafile; done
```

- tab completion: move to start of line using `^A` and end of line `^E` (option with arrows to move by one word)
- `history`: see old commands, find line number (repeat using !number)
- Socrative questions 7 and 8

## Shell Scripts

**Objectives:** write shell script to run command or series of commands for fixed set of files, run shell script from command line, write shell script to operate on set of files defined on command line, create pipelines including user-written shell scripts

- go back to molecules in nelle's directory
- create file called `middle.sh` and add this command: `head -15 octane.pdb | tail -5`
- `bash middle.sh`
- `.sh` means it's a shell script
- very important to make these in a text editor, rather than in word!
- edit `middle.sh` and replace file name with `"$1"`
- quotations accommodates spaces in filenames
- `bash middle.sh octane.pdb`, should get same output
- try another file: `bash middle.sh pentane.pdb`
- edit `middle.sh` with `head “$2” “$1” | tail “$3”`
- `bash middle.sh pentane.pdb -20 -5`
- to remember what you've done, and allow for other people to use: add comments to top of file

```bash
#select lines from middle of a file
#usage: middle.sh filename -end_line -num_lines
```

- explain comments

  - what if we wanted to operate on many files? create new file: `sorted.sh`
  - `wc -l “$@” | sort -n`
  - `bash sorted.sh *.pdb ../creatures/*.dat`
  - add comment!
  - save last few lines of history to file to remember how to do work again later:

- `history | tail -4 > redo-figure.sh`

- `history | tail -5 | colrm 1 7` (1-7 characters)

  - nelle problem

- run goostats on all data files

- `do-stats.sh`:

```bash
#calculate reduced stats for data files at J = 100 C/bp
  for datafile in “$@”
    do
      echo $datafile
      bash goostats -J 100 -r $datafile stats-$datafile
  done
```

- `bash do-stats.sh *[AB].txt`
- or just report `bash do-stats.sh *[AB].txt | wc -l`

  - Socrative question 9

## Finding Things

**Objectives:** grep to select lines in text which match patterns, find to find files whose names match patterns, nesting files, text vs binary files

- move to writing subdirectory
- `cat haiku.txt`
- `grep not haiku.txt` : find lines that contain "not"
- `grep day haiku.txt` : find lines that contain "day"
- `grep -w day haiku.txt` : searches only for whole words
- `grep -n it haiku.txt` : includes the numbers on lines that match
- `grep -n -w the haiku.txt` : combine flags
- `grep -n -w -i the haiku.txt` : make case insensitive
- `grep -n -w -v the haiku.txt` : invert selection, only lines that do NOT contain the
- the real strength of grep, and the origin of its name, is "regular expressions," which describes ways of programmatically describing text strings/search patterns, but we don't have time to cover these today (many awesome lessons and tutorials online)

**difference between grep and find**

- `find . -type d` : look for things that are directories in given path
- `find . -type f` : look for files instead
- find is automatically recursive (keeps drilling down into file hierarchy)

  - can specify depth: `find . -maxdepth 1 -type f`
  - or `-mindepth`

- can match by name: `find . -name *.txt` (will only give one filename! expands name prior to running command)

- correct way: `find . -name '*.txt'`

- find similar to list, but has more refined parameter searching

- can combine together: count all lines in a group of files

- `wc -l $(find . -name '*.txt')`

- nesting or subshell

- equivalent command: `wc -l ./data/one.txt ./data/two.txt ./haiku.txt`

- can also combine find and grep: find .pbd files that contain Iron

  - `grep FE $(find .. -name '*.pdb')`

- today we've only talked about text files, what about images, databases, etc? those are binary (machine readable)

- Socrative question 10

# END CLASS

- stop shell script output
