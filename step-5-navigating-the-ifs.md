# Step 5: Navigating the IFS

When you log in you are placed in a PASE shell and also into a directory in the IFS. Previously we used `pwd` to print the current working directory. Further, you can use the `ls` \(list\) command to display the contents of a directory.

## Try: `ls`

Try the `ls` command for yourself and you should see something like the below.

```text
~% ls
~%
```

Nothing was listed because the directory is empty. Well, that's only partially true. I just so happen to know there are "hidden" files in this directory. Hidden files start with a period and aren't displayed by default. Most all PASE commands have options that let you expound on what you want the command to do. The PASE commands delivered with the IBM i operating system lack what are called "man pages", or manual pages, the documentation for the command. Because of this we instead head to Google and search for "[ls command](http://linuxcommand.org/man_pages/ls1.html)".

In the documentation we see the `-a` option, as shown below.

```text
-a,
--all do not hide entries starting with .
```

Now re-run the `ls` command with the `-a` option.

```text
~% ls -a 
. 
.. 
.ssh 
.zprofile
```

As you can see there are two hidden entries, `.ssh` is a hidden directory and `.zprofile` is a hidden file. You'll also notice `.` and `..` \(a single and double period\). These are for when you want to use relative paths in your commands.

For example, if I wanted to change my current directory to that of my parent directory then I could issue the `cd` \(change directory\) command with two periods, as shown below.

```text
% cd .. 
/home%
```

Notice how this changes the current directory in my prompt to `/home`. Previously I was in my home directory \(i.e. `/home/USRZ8IGS`\) and it used home directory short form of `~`.

I can run the `ls` command again to see my home directory \(i.e. `USRZ8IGS`\) because it is a child directory of the `/home` directory.

```text
/home% ls USRZ8IGS
```

Change back to your "home" directory by issuing the following command.

```text
/home% cd -
```

Notice the command changed your prompt back to `~%` - the short form for the "home" directory.

Now try to list the contents of a directory that's further up the tree from where you're at - the root directory. The root is the single forward slash \(`/`\).

```text
~% ls / 
QOpenSys dev home opt tmp var bin etc lib sbin usr
```

Displaying the root \(`/`\) directory gives you perspective as to what might be installed. For example, if PowerRuby was installed you'd see a `/PowerRuby` directory. If I wanted to see what other open source tools were installed from IBM, I could do the following.

```text
~% ls 
/QOpenSys/QIBM/ProdData/OPS Python-pkgs Python2.7 Python3.4 tools
```

There are many more directories you can explore. Here's a nicely formatted listing showing two levels deep of each root-level directory.

```text
|-- QOpenSys 
|-- QIBM 
|-- bin → /QOpenSys/usr/bin 
|-- lib → /QOpenSys/usr/lib 
|-- litmis 
|-- opt 
|-- sbin → /QOpenSys/usr/sbin 
|-- usr
|-- bin -> /QOpenSys/usr/bin
|-- dev
|   `-- pts
|-- etc
|   |-- X11
|   `-- skel
|-- home
|   |-- AARON
|   `-- USRU4WY0
|-- lib -> /QOpenSys/usr/lib
|-- opt -> /QOpenSys/opt
|-- sbin -> /QOpenSys/usr/sbin
|-- tmp
|-- usr
|   |-- bin -> /QOpenSys/usr/bin
|   |-- include -> /QOpenSys/usr/include
|   |-- lib -> /QOpenSys/usr/lib
|   |-- linux
|   |-- sbin -> /QOpenSys/usr/sbin
|   `-- share -> /QOpenSys/usr/share
`-- var
```

**IMPORTANT:** The `/QOpenSys` file system is case sensitive! This is important to know as you continue to work through this lab because there is a difference between `/QOpenSys/mydir` and `/QOpenSys/Mydir`.

## Try: Symbolic Links

You'll notice some of them have `->` in front of them. This indicates that they're a symbolic link. Symbolic links are similar to Windows desktop shortcuts; they point to something elsewhere on the file system.

Go ahead and create your own symbolic link using the following `ln` command.

```text
% ln -s ~ /QOpenSys/myhome
```

Now use the `ls -al` to display the `/QOpenSys` directory so we can see the new symbolic link and where it points to.

```text
~% ls -al /QOpenSys total 128 
drwx------ 6 usru4wy0 0 8192 Apr 21 15:25 . 
drwx------ 9 usru4wy0 0 8192 Apr 21 09:08 .. 
drwx------ 3 usru4wy0 0 8192 Apr 21 09:05 QIBM 
lrwxrwxrwx 1 usru4wy0 0 34 Apr 21 09:07 bin → /QOpenSys/usr/bin 
lrwxrwxrwx 1 usru4wy0 0 34 Apr 21 09:07 lib → /QOpenSys/usr/lib 
drwx------ 4 usru4wy0 0 8192 Apr 21 09:08 litmis 
lrwxrwxrwx 1 usru4wy0 0 28 Apr 21 15:25 myhome → /home/USRU4WY0 
drwx------ 3 usru4wy0 0 8192 Apr 21 09:08 opt 
lrwxrwxrwx 1 usru4wy0 0 36 Apr 21 09:07 sbin → /QOpenSys/usr/sbin 
drwx------ 8 usru4wy0 0 8192 Apr 21 09:06 usr
```

Change directory into `/QOpenSys/myhome` and create a new file with some content, as shown below.

```text
~% cd /QOpenSys/myhome 
/QOpenSys/myhome% echo 'something' > file.txt
```

Now display the contents of your home directory using the `~` \(tilde\) approach - you should see the newly created `file.txt` file.

```text
/QOpenSys/myhome% ls ~ file.txt
```

Now run the below `cd` command to return to the immediate previous directory since the last time you ran `cd`.

```text
/QOpenSys/myhome% cd - 
~%
```

As you can see it returned you to your `~` \(home\) directory.

## Try: Locating Files

Sometimes you need to first locate a file before you do something with it. The `find` command works well for that.

The `find` [documentation](http://man7.org/linux/man-pages/man1/find.1.html) declares the following syntax.

```text
find [-H] [-L] [-P] [-D debugopts] [-Olevel] [starting-point...] [expression]
```

When you look at command documentation you should know that square brackets \(i.e. `[` and `]`\) denote optional parameters. In this case we're only interested in implementing `[starting-point...]` and `[expression]`.

Run the below command to locate a file named `file.txt` \(the expression\) located somewhere in the `/home` \(the starting point\) directory.

```text
~% find /home -name file.txt 
/home/USRU4WY0/file.txt
```

You can also do wildcards in the event you want a list of files, or aren't sure of the exact name. Run the following command.

```text
~% find /home -name '*\*.txt*' 
/home/USRU4WY0/file.txt
```

Notice the file name wildcard is now inside of quotes.

## Try: Locating Files with Specific Content

Next try to locate a file based on its content. To do that we use the `grep` command in combination with the `find` and `xargs` commands.

```text
~% find . -type f | xargs grep -i "something"
```

The first parameter of `find` is where to search. A single period declares to search in the current directory. The second parameter is the `-type` option declaring to process all files in the current and sub directories.

Next we see a vertical bar \( `|`\) also known as a pipe. This is passing \(piping\) the results from the `find` command to the next command, in this case `xargs`\(n1\). The `xargs` is a special command the formulates the results from the previous command and preps it for the next, in this case `grep`.

The `grep` command receives in the output from `xargs` \(which is a list of files to search through\) and it does a case-insensitive search \(`-i`\) for the string "something".

Give it a try in your home directory. You results should look like the following.

```text
~% find . -type f | xargs grep -i 'something' 
./file.txt:something 
./file.txt~:something
```

n1 - More `xargs` info [here](https://shapeshed.com/unix-xargs/).

## Please proceed to the next step.

