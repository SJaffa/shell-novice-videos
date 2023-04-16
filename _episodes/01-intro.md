---
title: "Introducing the Shell"
teaching: 5
exercises: 0
questions:
- "What is a command shell and why would I use one?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "A shell is a program whose primary purpose is to read commands and run other programs."
-  "This lesson uses Bash, the default shell in many implementations of Unix."
-  "Programs can be run in Bash by entering commands at the command-line prompt."
- "The shell's main advantages are its high action-to-keystroke ratio, its support for
automating repetitive tasks, and its capacity to access networked machines."
- "The shell's main disadvantages are its primarily textual nature and how
cryptic its commands and operation can be."
---

# Welcome & motivation

**SHOW** speaker

Welcome to this introduction to the UNIX shell course from UCL's Centre for Advanced Research Computing.

## Background

**SHOW** intro slides

Humans and computers commonly interact in many different ways, such as through a keyboard and mouse, touch screen interfaces, or using speech recognition systems.
The most widely used way to interact with personal computers is called a
**graphical user interface** (GUI).
With a GUI, we give instructions using the mouse to click on icons and menus.

While the visual aid of a GUI makes it intuitive to learn, this way of delivering instructions to a computer scales very poorly.
Imagine the following task: to analyse the data of a lot of samples you have taken, you have to copy the third line of one thousand text files in one thousand different directories and paste it into a single file.
Using a GUI, you would not only be clicking at your desk for several hours, but you could potentially also make a mistake in the process of completing this repetitive task.
This is where we take advantage of the Unix shell.
The Unix shell is both a **command-line interface** (CLI) and a scripting language, allowing such repetitive tasks to be done automatically and fast.
With the proper commands, the shell can repeat tasks with or without some modification as many times as we want.
Using the shell, the task in the literature example can be accomplished in seconds.

## Motivation

**SHOW** motivation slides

Why do we teach Unix shell to researchers?

After all, anyone who wants to rename several thousand data files can do so with any modern programming language like Python, and also do your data analysis and visualisation at the same time. So why do we need to learn an extra tool instead of using one language for everything?

Firstly, we teach the shell because it's an easy way to introduce some fundamental ideas about computer programming.
As we learn how to use the Unix shell, we we will cover many fundamental concepts in programming, such as getting the computer to repeat things, savingresearch workflows so you can repeat tasks later, and making your code easy to understand for your future self and anyone you share it with, by using comments nad sensible names for things..

The second answer is, "Because so much else depends on it."
Installing research software, configuring your default editor, and controlling remote machines frequently assume a basic familiarity with the shell, and with related ideas like standard input and output. (**SHOW** [tensorflow installation instructions](https://www.tensorflow.org/install/pip#linux))
Beacuse the shell has been around for so long, many tools also use its terminology (for example, the `%ls` and `%cd` magic commands in IPython) and conventions (e.g. why it's a bad idea to put spaces or * in filenames).

The third answer is, "Because it allows you to access many domain-specific tools and computing resources that researchers cannot access otherwise."
Familiarity with the shell is very useful for remote accessing machines, using high-performance computing infrastructure, and running new specialist tools in many disciplines.
When computing power is important, creating a graphical interface and processing mouse clicks is a waste of resources. A command line interface can run on a very old slow desktop computer, a tiny raspberry pi, or an expensive high performance system without slowing you down.
We do not teach HPC or domain-specific skills here but you might have been refered to this course if you are learning how to use UCL's High Performance Computers.

Finally, the shell is incredibly extendable and configurable so you can add all sorts of customisations and shortcuts (**SHOW** `tmux` with weather, stats, code) to make it work faster or better for your particular project, display useful information about you code, computer or the weather, and make it look like you are a cool hacker in the movies. (**SHOW** [hollywood](https://itsfoss.com/hollywood-hacker-screen/))

**SHOW** back to slides

Some disadvatages of using a command-line interface are that it can be hard to get started using the shell in your everyday work because you need to spend time learning the commands. Many commands have names that are not obvious, so you can't easily guess what `ls` or `cat` do.

Using the shell will take some time and effort to learn.
While a GUI shows you icons or menus to decide what you want to do, available CLI commands are not automatically presented to you, so you must learn a few commands like new vocabulary in a language you're studying.
However, a small number of "words" (i.e. commands) in Bash gets you a long way.
This course will cover the most important and commonly used commands, show you how to stick these small commands together like building blocks to make quite complex programs, and explain how to get help to learn new commands when you want to go further.

**SHOW** links to quizzes, terminology, tips and tricks, and further resources.

If you have already used a Bash shell before you can try the quizzes in this module to see if you already know what we are cvering in these videos. Any questions you get wrong will point you to the relevant parts of the course,  but we recommend everyone watches some of the videos that are listed here. These ones are especially important to make sure you are familiar with the terminology you need for later courses, and some hints and tips that will allow you to work faster in the shell.
We also have a list of more advanced shell tools, customisations and follow up courses if you want to go beyond the basics we teach here.

Let's get started.

# Terminology

## Unix

Unix is an operating system that was the forerunner of MacOS and Linux, so we call these Unix-like systems and they have a Unix shell installed already.
Windows developed in a different way so it has other kinds of command-line interfaces (you might have come across the command prompt or Windows Powersell).
You will need to install some extra software to allow you to use a Unix shell
Check out our setup instructions if you haven't done this already.

## Shell

A shell is a program where users can type commands.
With one line, you can do anything from simple commands like creating a new file to running complicated programs like climate modeling software.
We might also call this the Bash shell, terminal, or command prompt.

## Bash shell

The most popular Unix shell is Bash (the Bourne Again SHell --- so-called because it's derived from a shell written by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix and in most  packages that provide Unix-like tools for Windows.

There are other shells available. To check which one you are using, you can type

~~~
echo $SHELL
~~~
{: .language-bash}

and press enter -  the output should say "bash".
~~~
/bin/bash
~~~
{: .output}

If it says something else (you might see `zsh` or `tcsh` you need to go back to the setup instructions and check you have followed all the steps for your OS.)

In this course, whenever we say "the shell", we mean a Bash shell.

## GUI and CLI

The most widely used way to interact with personal computers is called a
**graphical user interface** (GUI).
A GUI displays some graphical elements such as menus, icon, or text boxes, and we interact with it by clicking a mouse, tapping a touch screen or typing.

A **command-line interface** (CLI) is 

TODO

# Tour of the shell

## Prompt

Open up your Bash shell and let's have a look around.
You should presented with a **prompt**, indicating that the shell is waiting for input.

~~~
$
~~~
{: .language-bash}

If you don't see this, the shell program may still be loading so wait a minute, or check our setup instructions again.

The shell typically uses `$ ` as the prompt, but may use a different symbol, and you might see some text before it.
In examples online,  people often show the prompt as `$ ` or `> ` when showing you what commands to type to install their software.

*You do not type the $ prompt* when typing commands, only the words, letters and symbols that follows the prompt.

## Words before the prompt

## Cursor

The prompt is followed by a **text cursor**, a character that indicates the position where your typing will appear.
The cursor is usually a flashing or solid block, but it can also be an underscore or a line.
You may have seen it in a text editor program, for example.

TODO: difference between line cursor and block. Mention insert key in word?

## Running your first command

When you have written the command, you have to press the <kbd>Enter</kbd> key to execute it.

So let's try our first command, `ls`, which is short for listing.
This command will list the contents of the current directory:

~~~
$ ls
~~~
{: .language-bash}

~~~
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
~~~
{: .output}

TODO first drafted up to here...

## Output or no output

## Errors

## Command not found
If the shell can't find a program whose name is the command you typed, it will print an error message such as:

~~~
$ ks
~~~
{: .language-bash}
~~~
ks: command not found
~~~
{: .output}
This might happen if the command was mis-typed or if the program corresponding to that command is not installed


## Nelle's Pipeline: A Typical Problem

Nelle Nemo, a marine biologist,
has just returned from a six-month survey of the
[North Pacific Gyre](http://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She has 1520 samples that she's run through an assay machine to measure the relative abundance
of 300 proteins.
She needs to run these 1520 files through an imaginary program called `goostats.sh`.
In addition to this huge task, she has to write up results by the end of the month, so her paper
can appear in a special issue of *Aquatic Goo Letters*.

If Nelle chooses to run `goostats.sh` by hand using a GUI,
she'll have to select and open a file 1520 times.
If `goostats.sh` takes 30 seconds to run each file, the whole process will take more than 12 hours
of Nelle's attention.
With the shell, Nelle can instead assign her computer this mundane task while she focuses
her attention on writing her paper.

The next few lessons will explore the ways Nelle can achieve this.
More specifically,
the lessons explain how she can use a command shell to run the `goostats.sh` program,
using loops to automate the repetitive steps of entering file names,
so that her computer can work while she writes her paper.

As a bonus,
once she has put a processing pipeline together,
she will be able to use it again whenever she collects more data.

In order to achieve her task, Nelle needs to know how to:
- navigate to a file/directory
- create a file/directory
- check the length of a file
- chain commands together
- retrieve a set of files
- iterate over files
- run a shell script containing her pipeline

{% include links.md %}
