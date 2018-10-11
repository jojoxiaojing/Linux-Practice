# Linux-Practice

## Linux Manual

Here is the link to linux manual: https://linux.die.net/man/

### Section Structure
* Section 1: user commands (introduction)
* Section 2: system calls (introduction)
* Section 3: library functions (introduction)
* Section 4: special files (introduction)
* Section 5: file formats (introduction)
* Section 6: games (introduction)
* Section 7: conventions and miscellany (introduction)
* Section 8: administration and privileged commands (introduction)

### Command Synopsis
|  Section      | Meaning                              |
| ------------- |:-------------:                       | 
|[THING]        |  THING is optional                   |
| \<THING\>     |  THING is mandatory (required)       |
|THING ...      | THING can be repeated (limitlessly)  |
|THING1         | THING2  | Use THING1 OR THING2. Not Both|
|*THING*        | [Notice the Italics] Replace THING   |


### The shell
One types commands to the shell, the command interpreter. It is not built-in, but is just a program and you can change your shell. The standard one is called sh. See also ash, bash, csh, zsh, chsh.

* **command prompt**
it is the shell's way of indicating that it is ready for the next command.
* **date** (that gives date and time)
* **cal** (that gives a calendar).
* **ls** lists the contents of the current directory
-l option it gives a long listing, that includes the owner and size and date of the file, and the permissions people have for reading and/or changing the file. 
* **cat** will show the contents of a file. (The name is from "concatenate and print")
* **cp** (from "copy") will copy a file. On the other hand, the command mv (from "move") only renames it.
* **diff** lists the differences between two files. Here there was no output because there were no differences.
* **rm** (from "remove") deletes the file, and be careful! it is gone. No wastepaper basket or anything. Deleted means lost.
* **grep** (from "g/re/p") finds occurrences of a string in one or more files. 

### Pathnames and the current directory
Pathname described the path from the root of the tree (which is called /) to the file. 

* **pwd** prints the current directory.

* **cd** changes the current directory. 

### Directories
* **mkdir** makes a new directory.
* **rmdir** removes a directory if it is empty, and complains otherwise.

* **find** (with a rather baroque syntax) will find files with given name or other properties. For example, "find . -name tel" would find the file "tel" starting in the present directory (which is called "."). And "find / -name tel" would do the same, but starting at the root of the tree. Large searches on a multi-GB disk will be time-consuming, and it may be better to use locate(1).

### Disks and filesystems
* **mount** will attach the file system found on some disk (or floppy, or CDROM or so) to the big file system hierarchy. 
* **umount** detaches it again. 
* **df** will tell you how much of your disk is still free.

### Processes
On a UNIX system many user and system processes run simultaneously. The one you are talking to runs in the **foreground**, the others in the **background**. 

* **ps** will show you which processes are active and what numbers these processes have. 
* **kill** allows you to get rid of them. Without option this is a friendly request: please go away. 
* **kill -9** followed by the number of the process is an immediate kill. 
* Foreground processes can often be killed by typing Control-C.

