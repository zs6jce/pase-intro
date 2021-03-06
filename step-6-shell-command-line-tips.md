# Step 6: Shell Command Line Tips

## Shell Command Line Tips

Before going further it would be good to teach you some short-cut key sequences that will aid in more easily navigating the shell command line.

### Short-cut keys

`Ctrl` + `A`: Go to beginning of line

`Ctrl` + `E`: Go to end of line

`Ctrl` + `U`: Cut current command and place into clipboard.

`Ctrl` + `C`: Terminate currently running command. Also works to clear the current line if you've typed a bunch of things but don't want to use it.

`Ctrl` + `R`: Search for previous command. This can be a short-cut to using `Up Arrow`.

`Up Arrow`: Load previous commands.

`Tab`: Press `tab` while you are in the middle of typing a directory or file and it will attempt to finishing typing the file name for you.

## Try `tab`

Try the following. Type in `cd /QO` and press the `tab` key.

```text
~% cd /QO
```

It should auto complete to the following.

```text
~% cd /QOpenSys/
```

Now type `cd /` and press the `tab` key.

```text
~% cd /   QOpenSys/ dev/ home/ opt@ tmp/ var/ bin@ etc/ lib@ sbin@
usr/
```

As you can see it expands out to show everything that exists in the root \(`/`\) of the IFS. Note it leaves your cursor right where you left it so you can immediately start typing the directory name of your choice.

## Try begin/end of line

A common scenario I'll have is listing a file's details and then subsequently need to run a different command on the same file. If your cursor is at the end of the line then that means you'll need to hold down the left arrow key until the cursor is at the beginning of the line. **Or** you can take a short-cut and type `Ctrl` + `A` to go to the beginning of the line.

Try the following. Type the full path to the below file and hit the `Enter` key. Don't forget to use your `tab` completion skills.

```text
~% ls -al /QOpenSys/QIBM/ProdData/OPS/tools/man/man1/zip.1
-rwx------ 1 usrmah25 0 85502 Jun 10 2016 /QOpenSys/QIBM/ProdData/OPS/tools/man/man1/zip.1
```

Press the up arrow to retrieve the most recently run command.

Now press `Ctrl` + `A` to place your cursor at the beginning of the line and replace `ls -al` with `head` and hit `Enter`.

```text
~% head /QOpenSys/QIBM/ProdData/OPS/tools/man/man1/zip.1 
." =========================================================================
." Copyright (c) 1990-2008 Info-ZIP. All rights reserved. 
." 
." See the accompanying file LICENSE, version 2007-Mar-4 or later 
." (the contents of which are also included in zip.h) for terms of use.
." If, for some reason, all these files are missing, the Info-ZIP license 
." also may be found at: <ftp://ftp.info-zip.org/pub/infozip/license.html>
." ==========================================================================
." 
." zip.1 by Mark Adler, Jean-loup Gailly and R. P. C. Rodgers
```

As you can see it printed out the top of the using the [`head`](http://www.computerhope.com/unix/uhead.htm) command.

Now press `Up Arrow` to retrieve the most recent command. Now try pressing `Ctrl` + `E` to return to the end of the line and then `Ctrl` + `A` to go to the beginning. Do that a couple times so you can become familiar to the keystrokes.

## Try: `Ctrl` + `R`

There will be times where using `Up Arrow` to retrieve a previously run command might entail going through a lot of commands. In that case you might try `Ctrl` + `R` which will bring up a prompt allowing you to search your shell history.

To try this, press `Ctrl` + `R` and type the beginning of one of the previous commands you've run. Below I've typed `ls` for the command.

```text
~% ls -al /QOpenSys/QIBM/ProdData/OPS/tools/man/man1/zip.1
bck-i-search: ls
```

Once the command you need to run has been loaded into the command line then press `Enter`.

### Please proceed to the next step.

