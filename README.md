# ce03 Multiuser System Fun Times

This class exercise is designed to familiarize students with file and directory permissions in a 
multiuser Unix environment.

## Prerequisite Knowledge

* Understanding of Unix basics, including commands, text editors, etc.
* Java packages.
* Unix Tutorial Five: http://www.ee.surrey.ac.uk/Teaching/Unix/unix5.html
* CSCI 1302 Octal Mode Reading: https://github.com/cs1302uga/cs1302-tutorials/blob/master/octal-mode.md

## Questions

In your notes, clearly answer the following questions. These instructions assume that you are 
logged into the Nike server. 

**NOTE 1:** For this exercise, at least two group members will need
access to Nike at the same time. When relevant, the instructions will refer to `user1`, `user2`, and `group` to indicate 
who should perform the actions for that step. Make sure you execute them in order.

**NOTE 2:** If a step requires you to enter in a command, please provide in your notes the full command that you 
typed to make the related action happen. If context is necessary (e.g., the command depends on your 
present working directory), then please note that  context as well.

### Multiuser Intro

1. `user1`: Launch a terminal emulator and create the subdirectory structure seen below. 
   In `Loop.java`, create the `cs1302.loop.Loop` class (fully qualified name) and write an infinite 
   loop in the `main` method.  
   You are free to do any sort of mathematical calculations you wish in
   the loop (or none at all), but the loop shouldn't print anything or take any user input.

   ```
   exercise3
    |--- src
          |--- cs1302
                |--- loop
                     |--- Loop.java
   4 directories, 1 file
   ```
   
1. `user1`: What is the size and mode of `Loop.java`?  Assuming your present working directory is `exercise3`, what exact command did you
use to find this?

1. `user1`: Compile `Loop.java` and then run it as a background process.

1. `user2`: Launch a terminal emulator on your laptop, connect to nike on your account (not the same account as `user1`).

1. `user2`: Find the Process ID (PID) of the executing `Loop.java` process from `user1`.
**Hint:** Try `ps` (maybe with a few options) to see every process in the system. You may need to filter the result with `grep`.

1. `user2`: Try to kill `user1`'s process. Were you able to successfully kill the process?  If not, why do 
think you were unsuccessful?

1. `user1`: Since `Loop.java` contains an infinite loop and is now running in the background, we will need to terminate it.  
Write at least two commands (or series of commands) to accomplish this.

**CHECKPOINT**
    
### File Permissions

1. `user1`: What is the mode of the `exercise3` directory in both octal and symbolic notation?

1. `user1`: Carefully change the permission of your home directory to add execute permission for
   other. Be very careful! If you mess up the user permissions on your home directory, then that
   can lead to unintended, bad consequences. Since this is a high stakes step, the exact recommended 
   command is provided below:
   
   ```
   $ chmod o+x ~
   ```
   
   This step is needed because student home directories on Nike are in a group that is different 
   from `ugrads`. Subdirectories of your home directory should belong to the `ugrads` group as expected.
   You can remove execute permission for other __at the end of this activity__ using:
   
   ```
   $ chmod o-x ~
   ```
   
1. `user2`: Can you successfuly perform an `ls` on `user1`'s `exercise3` directory?

1. `user1`: Disable group read and group execute permissions for `Loop.java`. Additionally, 
if needed, enable group write permission as well. 

1. **TRICKY** `user2`: Add a single line Java comment to the end of `Loop.java`. Yes, it is possible. 

1. `user1`: Delete `user2`'s message from `Loop.java`, save, then enable group read and group write persmissions
on `Loop.java`.

1. `user2`: fix `user1`'s `Loop.java` so that it is no longer an infinite loop.  Now, try to compile the program
to the same location that `user1` compiled to earlier. Were you able to successfully compile it?  If not, why do 
think you were unsuccessful?

**CHECKPOINT** 
    
### Directory Permissions

1. `user1`: Create a subdirectory within `exercise3` called `thoughts`. Inside of the `thoughts` directory, 
add a file called `notes.txt`. Explicitly set the mode for each of the following to the indicated octal:
   * `exercise3` --> 770
   * `exercise3/thoughts` --> 700
   * `exercise3/thoughts/notes.txt` --> 660

1. `group`: In your notes, create the following table:

   | Mode | a | b | c | d | e |
   |------|---|---|---|---|---|
   | 700  |
   | 710  |
   | 730  |
   | 750  |
   | 770  |
   
   **NOTE:** For a directory, read and write permission are generally only useful in conjunction with
   execute permission. For this reason, some modes were omitted. 

   Now, for each of the octal modes listed in the table, indicate whether or not `user2` is able to
   perform the actions listed below if `user1` sets `thoughts` to that mode. After each row, reset the
   modes and recreate files, if needed.

      * (a) Read `notes.txt` using `cat`.
      * (b) Delete `notes.txt`.
      * (c) List the contents of `thoughts` using `ls`.
      * (d) Add a new file to `thoughts` called `notes2.txt`.
      * (e) Use `cd` to change to `thoughts`.
   
1. `user1`: Explicitly set the mode for each of the following to the indicated octal (these are different from step 1):
   * `exercise3` --> 700
   * `exercise3/thoughts` --> 770
   * `exercise3/thoughts/notes.txt` --> 660

1. `group`: In your notes, create the following table:

   | Mode | a | b | c | d | e |
   |------|---|---|---|---|---|
   | 700  |
   | 710  |
   | 720  |

   Now, for each of the octal modes listed in the table, indicate whether or not `user2` is able to
   perform the actions listed below if `user1` sets `exercise3` to that mode. After each row, reset the
   modes and recreate files, if needed. **NOTE:** Unlike the previous, similar question, you are changing
   the mode for `exercise3` instead of `thoughts`.

      * (a) Read `notes.txt` using `cat`.
      * (b) Delete `notes.txt`.
      * (c) List the contents of `thoughts` using `ls`.
      * (d) Add a new file to `thoughts` called `notes2.txt`.
      * (e) Use `cd` to change to `thoughts`. 

1. In the previous question, you probably noticed something interesting about the row for mode 710.
Is the same set of actions possible with other modes? If so, list them. 

1. `group`: What permissions do you feel are appropriate for a user's home directory?
Explain your choice.

**CHECKPOINT** 

<hr/>

[![License: CC BY-NC-ND 4.0](https://img.shields.io/badge/License-CC%20BY--NC--ND%204.0-lightgrey.svg)](http://creativecommons.org/licenses/by-nc-nd/4.0/)

<small>
Copyright &copy; Michael E. Cotterell, Brad Barnes, and the University of Georgia.
This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> to students and the public.
The content and opinions expressed on this Web page do not necessarily reflect the views of nor are they endorsed by the University of Georgia or the University System of Georgia.
</small>
