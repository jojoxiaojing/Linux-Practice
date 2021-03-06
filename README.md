


# Chapter 1 - Linux Manual and some basic commands

Here is the link to linux manual: https://linux.die.net/man/

## Section Structure
* Section 1: user commands (introduction)
* Section 2: system calls (introduction)
* Section 3: library functions (introduction)
* Section 4: special files (introduction)
* Section 5: file formats (introduction)
* Section 6: games (introduction)
* Section 7: conventions and miscellany (introduction)
* Section 8: administration and privileged commands (introduction)

## Command Synopsis
|  Section      | Meaning                              |
| ------------- |:-------------:                       | 
|[THING]        |  THING is optional                   |
| \<THING\>     |  THING is mandatory (required)       |
|THING ...      | THING can be repeated (limitlessly)  |
|THING1         | THING2  | Use THING1 OR THING2. Not Both|
|*THING*        | [Notice the Italics] Replace THING   |


## The shell
One types commands to the shell, the command interpreter. It is not built-in, but is just a program and you can change your shell. The standard one is called sh. See also ash, bash, csh, zsh, chsh.

* **command prompt**
it is the shell's way of indicating that it is ready for the next command.
* **date** (that gives date and time)
* **cal** (that gives a calendar).
    cal 12 2017
    cal -A 1 -B 1 12 2017
* **ls** lists the contents of the current directory
-l option it gives a long listing, that includes the owner and size and date of the file, and the permissions people have for reading and/or changing the file. 
* **cat** will show the contents of a file. (The name is from "concatenate and print")
* **cp** (from "copy") will copy a file. On the other hand, the command mv (from "move") only renames it.
* **diff** lists the differences between two files. Here there was no output because there were no differences.
* **rm** (from "remove") deletes the file, and be careful! it is gone. No wastepaper basket or anything. Deleted means lost.
* **grep** (from "g/re/p") finds occurrences of a string in one or more files. 

## Pathnames and the current directory
Pathname described the path from the root of the tree (which is called /) to the file. 

* **pwd** prints the current directory.
* **cd** changes the current directory. 

## Directories
* **mkdir** makes a new directory.
* **rmdir** removes a directory if it is empty, and complains otherwise.
* **find** (with a rather baroque syntax) will find files with given name or other properties. For example, "find . -name tel" would find the file "tel" starting in the present directory (which is called "."). And "find / -name tel" would do the same, but starting at the root of the tree. Large searches on a multi-GB disk will be time-consuming, and it may be better to use locate(1).

## Disks and filesystems
* **mount** will attach the file system found on some disk (or floppy, or CDROM or so) to the big file system hierarchy. 
* **umount** detaches it again. 
* **df** will tell you how much of your disk is still free.

## Processes
On a UNIX system many user and system processes run simultaneously. The one you are talking to runs in the **foreground**, the others in the **background**. 

* **ps** will show you which processes are active and what numbers these processes have. 
* **kill** allows you to get rid of them. Without option this is a friendly request: please go away. 
* **kill -9** followed by the number of the process is an immediate kill. 
* Foreground processes can often be killed by typing Control-C.

## Getting information
**man** pages, (like this one), so that the command "man kill" will document the use of the command "kill" . The program man sends the text through some pager, usually less. Hit the **space bar** to get the next page, hit **q** to quit.

```
Question: How would you open the manual page for a command called updatedb  from section 8 of the manual?

Answer: man 8 updatedb
```

# Chapter 2 - Linux Input and Output

## Input
Input refers to any information that your program receives (or reads). Input to a Bash script can come from several different places:

* Command-line arguments (which are placed in the positional parameters)
* Environment variables, inherited from whatever process started the script
* Files
* Anything else a File Descriptor can point to (pipes, terminals, sockets, etc.). This will be discussed below.

## Output
Output refers to any information that your program produces (or writes). Output from a Bash script can also go to lots of different places:

* Files
* Anything else a File Descriptor can point to
* Command-line arguments to some other program
* Environment variables passed to some other program


## Standard input and output
* 0 standard input
* 1 standard output
* 2 standard error

## Redirection
Before a command is executed, its input and output may be redirected using a special notation interpreted by the shell.
* \> means overwirting 
* \>> means append to the original file

\> is used to redirect the output, such as we can redirect the result into a file

```
$ cat 1> output.txt
Linux is amazing
ctrl + c
```
or

```
$ cat > output.txt
Linux is amazing
ctrl + c
```

or

we can also redirect the error into a file

```
$ cat -k bla 2>> error.txt
```

or

We can redirect standard output and error in the same time

```
$ cat 1>> output.txt 2>>error.txt
Linux is amazing!
ctrl + C
```

How to use redirect to read from a file

```l
$ cat > input.txt
Hello World!
Ctrl + C

$ cat < input.txt
Hello World!
```

How to redirect between 2 windows

```l
#Open a new window
#Input $ tty, and it will return the code of this window
$ tty
/dev/pts/1

#In another window
$ cat 0< input.txt > /dev/pts/1
```


## Piping

* Piping connects STDOUT of one command to the STDIN of another.
* Redirection of STDOUT breaks pipelines.
* To save a data "snapshot" without breaking pipelines, use the tee command.
* If a command doesn't accept STDIN, but you want to pipe to it, use xargs.

```
date | cut -d " " -f 1
date | cut -d " " -f 1 > today.txt
date | cut > today.txt -d " " -f 1 #the order of > today.txt does not matter
```

combine piping

```
date | tee fulldate.text | cut -d " " -f 1
date | tee fulldate.text | cut -d " " -f 1 >today.txt
```

how to pipe some commands that do not accept standard input, such as echo

```
date | xargs echo
: Mon 16 Oct ...
date | xargs echo "hello"
: hello Mon 16 Oct....
```
How to delete the files with name inside a file: use xargs

```
cat filestododelete.txt
: fulldate.txt
: today.txt
cat filestododelete.txt | xargs rm
```

## alias

in .bash_profile (for mac) .bash_aliases(for linux)， edit and save

```
$ cd ~
$ nano .bash_profile
$ source ~/.bash_profile
```

```
alias getdates='date | tee /Users/Jojo/Documents/Project/7.\ Linux\ Pratice/fulldate.txt | cut -d " " -f 1 | tee /Users/Jojo/Documents/Project/7.\ Linux\ Pratice/shortdate.txt | xargs echo hello'
```

## Exercise

```
ls /etc > file1.txt
ls /run > file2.txt
cat file1.txt file2.txt | tee unsorted.txt | sort -r unsorted.txt > reversed.txt
```



# Parameters

```linux
$ varname=vardata
#Cannot use spaces around the = sigm
```




