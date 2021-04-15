---
title: Intro to Bash Shell
date: April 2021
author: Tim Dennis
---

# UCLA Data Science Center - Intro to Shell

[![hackmd-github-sync-badge](https://hackmd.io/5oziF2v5TuiTcS1I3kCe3Q/badge)](https://hackmd.io/5oziF2v5TuiTcS1I3kCe3Q)


## Before class:

- set up shell:
  - `exec bash` - switches to bash from zsh
      - no longer needed on mac as zsh is default
  - enlarge text size - via preferences
  - `export PS1='$ '`
  - `export PROMPT_COMMAND="history 1 >> ~/Dropbox/UnixHistory.txt"`
  - Turn off the text coloring in terminal (`Terminal -> Preferences -> ANSI`)
  - students check software installation: `Unix`, git for windows
- Etherpad link: https://pad.carpentries.org/2021-ucla-spring-unix
- Get data for workshop: <http://swcarpentry.github.io/shell-novice/data/data-shell.zip>
- Unzip and put on desktop

## Checklist for class:

- mixed audience, both novice/experienced and disciplines
- if material is review for you, help by keeping notes on etherpad and helping your neighbor
- scientific computing has a long history of being self taught, so most instructors even learn something new

## Setup

- Most tasks in the shell can be done with mouse on Desktop. **Why do anything differently?**
- **Motivation**
- Unix == created before most in this class were born
- A way to combine powerful tools together using minimal keystrokes
- Let's us automating repetitive tasks: moving & processing files/data, run our research analysis, build applications 
- Often required to use in high performance computing & cloud computing
- Might be good for brief exercise in etherpad: jargon around command line, bash, etc.? 

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

1. you type something - LOOP
2. computer reads it - READ
3. executes command - EVAL
4. prints output - PRINT

* We use **command shell** to make this happen: this is the interface between user and computer
* bash: Bourne again shell, most commonly used, default on most modern implementations
* zsh - a variant of bash, now default on mac, for us today bash and zsh are interchangable 

## Scenario set up for lesson (optional)
NOTE: I often skip this

- Our friend Nelle has six months worth of survey data collected from the North Pacific
- 300 samples of **goo**
- Her pipeline:

1. Determine the abundance of 300 proteins
2. Each sample has one output file with one line for each protein
3. calculate statistics for each protein separately using program `goostat`
4. compare statistics for proteins using program called `goodiff`
5. write up results and submit by end of month

- If she enters all commands by hand, will need to do **45,150 times**.
- What can she do instead? Use the command line

### Benefits of the CLI:
- Automate repetitive tasks (**30 minutes** vs. **2 weeks**)
- Prevent user error, manual error
- Processing pipelnes are re-usable and sharable
- _REPL_ Read-Evaluate-Print-Loop, let's you interactively work things out

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

* let's see where we are in our file system

```bash
pwd
```

* `pwd` stands for print working directory, in this case it is also the home directory
* note that the home directory will look different on different OS's
* To understand "home directory" let's look at an image 

![Directory structure](http://swcarpentry.github.io/shell-novice/fig/filesystem.svg)

- root directory: holds everything else, begins with slash `/`
- structure of directories are below  that in a tree type structure 
- slashes `\` can also be a separator between names
- `ls` listing, prints names of files and directories in current directory and prints in alphabetical order

```bash
ls
```

- make the output more comprehensible by using the **flag**`-F`

```bash
ls -F
```

- `-F` adds trailing / to names of directories (note: on git for bash there's )
- spaces and capitalization in commands are important!
- `-F` is an **option, argument, or flag**
- `ls` has lots of other options. Let's find out what they are by:

```bash
ls --help
```

* many bash commands and programs support a `--help` flag to display more information
* for even more detailed information on how to usr `ls` type `man ls` (caveat WINDOWS users)
* `man` is for manual and prints the description of a command and options
* Git for Windows doesn't come with the `man` files, instead do a web search for `unix man page COMMAND`
* to navigate `man` files use the up and down arrows, or space bar and b for paging, to quit `q`


- We can also `ls` to see contents of another directory:

```bash
ls -F Desktop
```

- we `ls -F` to the Desktop from our home directory and we see the `data-shell/` folder we unziped there earlier
- let's look inside `data-shell`

```bash
ls -F Desktop/data-shell
```

- Let's change directories into that folder
- What do you think the command is for changing directories?
    - Yes, `cd`

```bash
cd Desktop
cd data-shell
cd data
```

- see where we are:

```bash
pwd
```

```bash
ls -F
```

- We can go down the directory structure, how do we go up?
- We might try:

```bash
cd data-shell
```

- `data-shell` is a level above our current location, but we can go up a level this way
- but there are different ways to navigate to directories above your current `pwd`

```bash
cd ..
```

- `..` goes up one level in file hierarchy
- `..` is special directory name meaning "the dir containing this one" (parent)
- let's confirm it worked: 

```bash
pwd
```

- `..` won't show up using `ls` by itself
- but we can do this to see hidden files:

```bash=hiddenfiles
ls -F -a
```

- `-a` shows hidden files, including `.` and `..`
- `-a` stands for show all
- `.` is for current directory, this can be useful if you want to reference your current location in the file system

* What happens if we type `cd` by itself? go ahead and do this and type in the chat what it does

```bash
cd
```

- by itself will return you to your `home` directory
- `pwd`
- how do we get back to our `data` folder?

```bash
cd Desktop/data-shell/data
```

- we can string together a list of directories at once
- so far we have been using **relative paths** paths starting from our current directory
- we can also use **absolute paths** in `ls` and `cd`

```bash
cd /Users/nelle/Desktop/data-shell
```

```bash
pwd
```

- two more short cuts: `~` and `-`
- challenges: open: <http://swcarpentry.github.io/shell-novice/02-filedir/#absolute-vs-relative-paths>

## Working With Files and Directories

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

- don't use whitespaces - whitespaces break arguments on CLI unless quoted, avoid, use `-` or `_` (or combination)
- don't start a name with `-`
    - commands treat names starting with `-` as options
- stay with letters, numbers, `-` and `_`
- if you need to refer to names of files or directories that have whitespaces, quote them

```bash=changethesis
cd thesis
ls -F
```

- nothing inside our new dir yet
- let's change directory to inside the `thesis` and create a file called `draft.txt`

```bash=create_draft
nano draft.txt
```
![](http://swcarpentry.github.io/shell-novice/fig/nano-screenshot.png)

- Creates file, opens text editor
- Editors are like cars -- everyone wants to customize them, so there are hundreds if not thousands of different models
- Write some text
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
- **Deleting is forever!**
- Let's recreate the file then move up one directory

```bash
nano draft.txt
cd ..
```

* now let's try and remove a directory
* removing a directory:

```bash=remove
rm thesis # error
rmdir thesis # still get error
rm thesis/draft.txt
rmdir thesis
```

* could've also used `rm -r thesis`, but that can be dangerous!

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

- first part of `mv` is what you want to move, second is to where and including the new name
- **note**: `mv` works on directories as well
- let's move `quotes` into the current directory. What does `.` mean? 

```bash
mv thesis/quotes.txt .
```

```bash
ls thesis
```

- `ls <filename>` will only list that file, let's see that our file is there

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

**Objectives:** redirect command output to file, construct pipelines

- now we can move around and create things, let's see how we can combine existing programs in new ways
- Let's got into the molecules directory

```bash
ls molecules
```

```bash
cd molecules
```

- the `.pdb` format indicates these are [Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank) files
- Let’s run an example command `wc` on cubane.pdb:

```bash
wc *.pdb
```

- we haven't covered the `*` yet. It is a wild card operator
- the `*` matches zero or more characters, so the shell turns `*.pdb` into a list of all `.pdb` files
- word count: lines, words, characters

### wc and flags

```bash
wc -l *.pdb
```

- only report number of lines
- what if we do this? what do you think will happen?

```bash
wc -l *.pdb > lengths.txt
```

- this will send output (redirect it) to new file named lengths.txt
- but let's confirm that it worked by using a new command `cat` - let's us look inside the file
- `cat` stands for concatenate

```bash
cat lengths.txt
```

- can't remember how wc reports? use `man wc` (`q` to exit), `wc -h`, or `wc –help` (this should work for most unix commands), also google `unix man wc`

### Sorting 

- now let's use the `sort` command to sort the contents of our file
- let's look at some options for `sort`

```bash=mansort
man sort
sort --help
```

- we will use the `-n` flag to tell sort to sort by numerical rather than alpha

```bash
sort -n lengths.txt
```
compare to: 

```bash=sort
sort lengths.txt
```

- sort by first column, using numerical order
- does not change file, just prints output to screen
- if we want to save results, what can we use? 
- yes, we use our rediretion operator `>` to save to file

```bash
sort -n lengths.txt > sorted-lengths.txt
```

- arrow up to recall last few commands
- let's use head to see the biggest:

```bash
head -1 sorted-lengths.txt
```

### Piping 

- Saving intermediate files like `sorted-lengths.txt` can get messy and confusing
- We can make it easier to understand by combining these commands together

```bash=pipe
sort -n lengths.txt | head -n 1
```

- **vertical bar** is the pipe in unix 
- it sends output of command on left as input to command on right
- `head` prints specified number of lines from top of file
- we can chain multiple commands together 
- for example send the output of `wc` directly to `sort`, and then the resulting output to `head`

```bash=pipe
wc -l *.pdb | sort -n
```
* adding `head` the full pipeline becomes:

```bash=full
$ wc -l *.pdb | sort -n | head -n 1
```

* this pipe and filter programming model is important conceptually
- note: you only enter the original files once!
- let's review what we covered via this image: 

![](http://swcarpentry.github.io/shell-novice/fig/redirects-and-pipes.svg)


### Nelle's pipeline (skip for time):

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
- first, let's looking at first three lines in each file

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
- strategy: `echo` command before running to make sure the loop is functioning the way you expect
- going back to the original file copying problem, we can solve this with the following loop:

```bash
for filename in *.dat
do
  cp $filename original-$filename
done
```
### Nelle's example (skip for time contraints)

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
