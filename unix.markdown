# Unix

Files and Directories
------------------------------
* `ls` 						# lists documents in current directory
* `cp <x> <y>` 		# copy <x> to <y>
* `mv <x> <y>`		# move <x> to <y>
* `rm <x>`				# remove file <x>
* `mkdir <x>` 		# makes new directory <x>
* `pwd` 					# shows current directory
* `cd <x>`				# goes into folder <x>
* `ln -s <x> <y>`	# makes a soft link between real file <x> and pointer <y>
* `cat <file>` 		# list the whole file
* `more <file>` 	# types <file> in chunks, <space> goes to next chunk
* `less <file>`		# similar to more
* `head -N <file>` 	# types the first N lines (flag-free default is 10?)
* `tail -N <file>`	# types the last N lines (flag-free default is 10?)

Globbing
--------
`*`									# wildcard (any number of chars)
`?`									# wildcard (one car)
`vim file.{h,cpp}`	# open file.h, file.cpp with vim (contrast w/ `vim file.*`)

In-line scripting
-----------------
```
for file in `ls`; do md5sum $file; done     # call md5sum on * in the dir
```


Math
-------
```
bc				# Calculator program
$ echo "obase=16; 15" | bc
F
$ echo "obase=2; 15" | bc
1111
$ echo "scale=3; 1/5" | bc
.200
```

Quoting
---------
Single quotes treat their contents literally, double quotes allow the shell to
evaluate shell constructs.

Escaping & Special Characters
--------------------------------------------
```
echo a*			  # wildcard
echo a\*			# literal asterisk
echo 'I live in $HOME'
echo "I live in $HOME"
echo "I live in \$HOME"
echo "There is a tab between here^V^I and here." # Use ^V to access the tab (^I)
```

Editing
----------
```
set -o vi			  # Use vim keystrokes to edit the command line (use <esc> to
	              # enter Normal Mode, <i> to return to Insert Mode).
set -o emacs		# Use emacs keystrokes to edit the command line
```

Fix Windows-style newline characters (translate to Unix-style)
-----------------------------------------------------------------------------------
```
tr '\r' '\n' < file.txt > file.txt
```

Redirection
------------------
```
some command < infile
some command > outfile      			  # create / overwrite
some command >& outfile				      # errors from command go to file
some command >> outfile     			  # Append
some command >>& outfile				    # appends error of command onto end of file
some command 2> errorfile   			  # Create / overwrite
come command > outfile 2> errorfile	# output and error stream in separate files
```

Combining Commands
--------------------------------
```
com1 ; com2 ; com3
com1 && com2 && com3    # stop if any in the sequence fails
com1 || com2 || com3    # stop as soon as any one succeeds
```

Process Management
---------------------------------
```
CTL-Z	    # pause the current process and return to console
bg 		    # allow the process you just paused to run in background
fg		    # move a background process to the foreground
jobs 	    # shows what you're running
ps 		    # shows processes
```

Help
----
```
man <c>        # help on command <c>
<c> -h	 	     # sometimes has help this way as well
<c> --help	   # sometimes has help this way as well, verbose flag style
```

Special Startup/Config Files
----------------------------
```
.login or .profile    # runs on login
.shrc or .cshrc       # runs when you invoke a script
```

Editing and Strings
-------------------
```
sed s/<a>/<b>/ <file> >
grep <a> <b>             # print out all lines in  <b> which contain string <a>
sort <a>                 # sort the file a
diff <a> <b>             # print out the difference between <a> and <b>
xemacs <a>               # edit the file <a>
```

Finding
-------
```
find .									                      # Recursive listing
find . -name CVS -type d -exec rm -rf {} \;   # Find & remove all dirs named CVS; start "here."
find . -name *.o -type f -exec echo {} \;	    # List all files named *.o; start "here."
find . -name ._* -type f -exec echo {} \;	    # List all files named ._*; start "here."
find . -name ._* -type f -exec rm {} \;       # Find & list all files named ._*; start "here."
mdfind                                        # Mac OSX only - use Spotlight registry for speed.
locate <file>                                 # w/o globbing, treated as "*foo*" (faster, but
                                              # possibly out of date).
```

Finding and removing recipe
----------------------------
```
cd /mydirectory
touch -t 1406181700 compare       # choose an appropriate reference time
find . -not -newer compare -name "*.*" -exec rm {} \;
rm compare
```

Searching
---------
```
grep -n {pattern} *				# Search all local files for {pattern} & print line numbers.
grep -i {pattern} *				# Perform a case insensitive search.
```

Files
-------
```
~> cat > myfile.txt
Line 1
Line 2
<ctrl-d>
~> cat >> my file.txt
<to append to the end>
```

Look at Files
-------------
```
head -n 1 *.py					          # Look at the first line of all .py scripts here.
tail -n 20 myfile.txt				      # Look at the last 20 lines of my file.txt.
watch -n 1 "tail -n 10 job.log"	  # Every second, look at the last 10 lines of job.log.
```

Killing Programs
----------------
```
^c        				# <ctrl>-c; Cancel; only works within shells
kill PID					# kill process ID.
^j        				# Get a shell prompt in a frozen window.
reset ^j					# Reset to reset state (may also need ^j)
```

Terminating a Shell
-------------------
```
^d
exit
```

Environmentals
--------------
This depends on what shell you are using. In the bash shells scripts use:
```
export <X>=<y> 		        # will make $X refer to <y>
export PATH=<y>:${PATH} 	# will append <y> to $PATH
```

In the c-shells csh and tcsh:
```
setenv <x> <y>   # is the same thing as export <x>=<y>
env 		         # will list all environmentals you have set
echo $ENV 	     # will print the value of $ENV to the terminal
```

Important Environmentals:
```
$HOST
$USER
$HOME               # your home area
$PWD                # the current directory
$PATH               # where unix looks for code to execute
$PYTHONPATH         # where unix looks for python modules to import
$LD_LIBRARY_PATH    # where unix looks for shared libraries
```

You normally want to append to the PATHs. Just setting them to <x>
wipes out all the other stuff they were already set to:
```
echo $LD_LIBRARY_PATH | tr \: \\n    # Show the $PATH nicely, one per line
echo ${USER:0:1}                     # print the first char of user
echo ${USER:0:2}                     # print the first two chars of user
echo ${USER#?}                       # print all but the first char of user
```

Aliases
-------
Edit .bashrc / .bash_profile : `alias minerva01="ssh perdue@minerva01.fnal.gov"`
Check with, e.g.: `$ type minerva01`


Miscellaneous Useful
--------------------
```
man ascii            # Print a table of all the ascii codes
cal                  # Bring up a calendar
xxd	somefile.bin		 # Examine hex dump of a binary file (somefile.bin)
od -x somefile.txt   # Examine hex dump of a file (can also do octal, decimal, ASCII)
lsb_release -a       # Details about "linux release base"
```

Look at Compiled Binary
-----------------------
```
strings -a a.out | grep -i gcc     # see what compiler was used
```

-------- top memory plot ---------
Here are instructions (that Trung gave me) to create the plots:
While running the program also run:  top -b -d 1 -u tice >> log.txt
When the program is done trim out the lines relevant to your executable: grep -e <exec name> log.txt | awk '{print NR " " $5}' | sed s/"m"/""/g > log.dat
Start gnuplot to make the plot: gnuplot
gnuplot> plot "log.dat" title "This is the title"

If you have two log.dat files, you can plot them together
gnuplot> plot "log_1.dat" title "This is title 1", \
               plot "log_2.dat" title "This is title 2"
