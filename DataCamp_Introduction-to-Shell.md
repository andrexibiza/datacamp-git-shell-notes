---
title: "DataCamp - Introduction to Shell"
instructor: [Filip Schouwenaars](https://www.datacamp.com/instructors/filipsch)
date: 2025-03-02
url: "https://app.datacamp.com/learn/courses/introduction-to-shell"
---

# Chapter 1: Manipulating Files and Directories

## How does the shell compare to a desktop interface? 

An [**operating system**]{.underline} like Windows, Linux, or Mac OS is a special kind of program. It controls the computer's processor, hard drive, and network connection, but its most important job is to run other programs.

Since human beings aren't digital, they need an interface to interact with the operating system. The most common one these days is a [**graphical file explorer**]{.underline}, which translates clicks and double-clicks into commands to open files and run programs. Before computers had graphical displays, though, people typed instructions into a program called a [**command-line shell**]{.underline}. Each time a command is entered, the shell runs some other programs, prints their output in human-readable form, and then displays a prompt to signal that it's ready to accept the next command. (Its name comes from the notion that it's the "outer shell" of the computer.)

Typing commands instead of clicking and dragging may seem clumsy at first, but as you will see, once you start spelling out what you want the computer to do, you can combine old commands to create new ones and [*automate repetitive operations*]{.underline} with just a few keystrokes.

## **Where am I?**

The **filesystem** manages files and directories (or folders). Each is identified by an **absolute path** that shows how to reach it from the filesystem's **root directory**: `/home/repl` is the directory `repl` in the directory `home`, while `/home/repl/course.txt` is a file `course.txt` in that directory, and `/` on its own is the root directory.

To find out where you are in the filesystem, run the command `pwd` (short for "**p**rint **w**orking **d**irectory"). This prints the absolute path of your **current working directory**, which is where the shell runs commands and looks for files by default.

## **How can I identify files and directories?**

`pwd` tells you where you are. To find out what's there, type `ls` (which is short for "**l**i**s**ting") and press the enter key. On its own, `ls` lists the contents of your current directory (the one displayed by `pwd`). If you add the names of some files, `ls` will list them, and if you add the names of directories, it will list their contents. For example, `ls /home/repl` shows you what's in your starting directory (usually called your **home directory**).

## **How else can I identify files and directories?**

An **absolute path** is like a latitude and longitude: it has the same value no matter where you are. A **relative path**, on the other hand, specifies a location starting from where you are: it's like saying "20 kilometers north".

As examples:

-   If you are in the directory `/home/repl`, the **relative** path `seasonal` specifies the same directory as the **absolute** path `/home/repl/seasonal`.

-   If you are in the directory `/home/repl/seasonal`, the **relative** path `winter.csv` specifies the same file as the **absolute** path `/home/repl/seasonal/winter.csv`.

The shell decides if a path is absolute or relative by looking at its first character: If it begins with `/`, it is absolute. If it *does not* begin with `/`, it is relative.

## **How can I move to another directory?**

Just as you can move around in a file browser by double-clicking on folders, you can move around in the filesystem using the command `cd` (which stands for "change directory").

If you type `cd seasonal` and then type `pwd`, the shell will tell you that you are now in `/home/repl/seasonal`. If you then run `ls` on its own, it shows you the contents of `/home/repl/seasonal`, because that's where you are. If you want to get back to your home directory `/home/repl`, you can use the command `cd /home/repl`.

## **How can I move up a directory?**

-   `..` = move up a directory

-   `.` = current directory

-   `~` = home directory

The **parent** of a directory is the directory above it. For example, `/home` is the parent of `/home/repl`, and `/home/repl` is the parent of `/home/repl/seasonal`. You can always give the absolute path of your parent directory to commands like `cd` and `ls`. More often, though, you will take advantage of the fact that the special path `..` (two dots with no spaces) means "the directory above the one I'm currently in". If you are in `/home/repl/seasonal`, then `cd ..` moves you up to `/home/repl`. If you use `cd ..` once again, it puts you in `/home`. One more `cd ..` puts you in the *root directory* `/`, which is the very top of the filesystem. (Remember to put a space between `cd` and `..` - it is a command and a path, not a single four-letter command.)

A single dot on its own, `.`, always means "the current directory", so `ls` on its own and `ls .` do the same thing, while `cd .` has no effect (because it moves you into the directory you're currently in).

One final special path is `~` (the tilde character), which means "your home directory", such as `/home/repl`. No matter where you are, `ls ~` will always list the contents of your home directory, and `cd ~` will always take you home.

## **How can I copy files?**

You will often want to copy files, move them into other directories to organize them, or rename them. One command to do this is `cp`, which is short for "copy". If `original.txt` is an existing file, then:

```         
cp original.txt duplicate.txt 
```

creates a copy of `original.txt` called `duplicate.txt`. If there already was a file called `duplicate.txt`, it is overwritten. If the last parameter to `cp` is an existing directory, then a command like:

```         
cp seasonal/autumn.csv seasonal/winter.csv backup 
```

copies *all* of the files into that directory.

## **How can I move a file?**

While `cp` copies a file, `mv` moves it from one directory to another, just as if you had dragged it in a graphical file browser. It handles its parameters the same way as `cp`, so the command:

```         
mv autumn.csv winter.csv .. 
```

moves the files `autumn.csv` and `winter.csv` from the current working directory up one level to its parent directory (because `..` always refers to the directory above your current location).

## **How can I rename files?**

`mv` can also be used to rename files. If you run:

```         
mv course.txt old-course.txt 
```

then the file `course.txt` in the current working directory is "moved" to the file `old-course.txt`. This is different from the way file browsers work, but is often handy.

One warning: just like `cp`, `mv` will overwrite existing files. If, for example, you already have a file called `old-course.txt`, then the command shown above will replace it with whatever is in `course.txt`.

## **How can I delete files?**

We can copy files and move them around; to delete them, we use `rm`, which stands for "remove". As with `cp` and `mv`, you can give `rm` the names of as many files as you'd like, so:

```         
rm thesis.txt backup/thesis-2017-08.txt 
```

removes both `thesis.txt` and `backup/thesis-2017-08.txt`

`rm` does exactly what its name says, and it does it right away: unlike graphical file browsers, the shell doesn't have a trash can, so when you type the command above, your thesis is gone for good.

## **How can I create and delete directories?**

`mv` treats directories the same way it treats files: if you are in your home directory and run `mv seasonal by-season`, for example, `mv` changes the name of the `seasonal` directory to `by-season`. However, `rm` works differently.

If you try to `rm` a directory, the shell prints an error message telling you it can't do that, primarily to stop you from accidentally deleting an entire directory full of work. Instead, you can use a separate command called `rmdir`. For added safety, it only works when the directory is empty, so you must delete the files in a directory *before* you delete the directory. (Experienced users can use the `-r` option to `rm` to get the same effect; we will discuss command options in the next chapter.)

Since a directory is not a file, you must use the command `mkdir directory_name` to create a new (empty) directory.

# Chapter 2: Manipulating Data

## **How can I view a file's contents?**

Before you rename or delete files, you may want to have a look at their contents. The simplest way to do this is with `cat`, which just prints the contents of files onto the screen. (Its name is short for "concatenate", meaning "to link things together", since it will print all the files whose names you give it, one after the other.)

```         
cat agarwal.txt 
```

```         
name: Agarwal, Jasmine position: RCT2 start: 2017-04-01 benefits: full
```

# **How can I view a file's contents piece by piece?**

You can use `cat` to print large files and then scroll through the output, but it is usually more convenient to **page** the output. The original command for doing this was called `more`, but it has been superseded by a more powerful command called `less`. (This kind of naming is what passes for humor in the Unix world.) When you `less` a file, one page is displayed at a time; you can press spacebar to page down or type `q` to quit.

If you give `less` the names of several files, you can type `:n` (colon and a lower-case 'n') to move to the next file, `:p` to go back to the previous one, or `:q` to quit.

Note: If you view solutions to exercises that use `less`, you will see an extra command at the end that turns paging *off* so that we can test your solutions efficiently.

## **How can I look at the start of a file?**

The first thing most data scientists do when given a new dataset to analyze is figure out what fields it contains and what values those fields have. If the dataset has been exported from a database or spreadsheet, it will often be stored as **comma-separated values** (CSV). A quick way to figure out what it contains is to look at the first few rows.

We can do this in the shell using a command called `head`. As its name suggests, it prints the first few lines of a file (where "a few" means 10), so the command:

```         
head seasonal/summer.csv 
```

displays:

```         
Date,Tooth 
2017-01-11,canine 
2017-01-18,wisdom 
2017-01-21,bicuspid 
2017-02-02,molar 
2017-02-27,wisdom 
2017-02-27,wisdom 
2017-03-07,bicuspid 
2017-03-15,wisdom 
2017-03-20,canine 
```

## **How can I type less?**

One of the shell's power tools is **tab completion**. If you start typing the name of a file and then press the tab key, the shell will do its best to auto-complete the path. For example, if you type `sea` and press tab, it will fill in the directory name `seasonal/` (with a trailing slash). If you then type `a` and tab, it will complete the path as `seasonal/autumn.csv`.

If the path is ambiguous, such as `seasonal/s`, pressing tab a second time will display a list of possibilities. Typing another character or two to make your path more specific and then pressing tab will fill in the rest of the name.

## **How can I control what commands do?**

You won't always want to look at the first 10 lines of a file, so the shell lets you change `head`'s behavior by giving it a **command-line flag** (or just "flag" for short). If you run the command:

```         
head -n 3 seasonal/summer.csv 
```

`head` will only display the first three lines of the file. If you run `head -n 100`, it will display the first 100 (assuming there are that many), and so on.

A flag's name usually indicates its purpose (for example, `-n` is meant to signal "**n**umber of lines"). Command flags don't have to be a `-` followed by a single letter, but it's a widely-used convention.

Note: it's considered good style to put all flags *before* any filenames, so in this course, we only accept answers that do that.
