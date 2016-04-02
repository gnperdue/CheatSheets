Misc
----

    list                      Show the code surrounding the current line of execution.
    disassemble               Look at the machine code.

Macros
------

    show user                 List all macros.

Example:

    (gdb) define print_and_go
    Type commands for definition of "print_and_go".
    End with a line saying just "end".
    >printf $arg0, $arg1
    >continue
    >end

Breakpoints
-----------

Stop execution at a point in the code.

    save-breakpoints <file>   Save current set of breakpoints.
    source <file>             Load the saved breakpoints.
    
    break <line number>       Set a breakpoint at line number in the current file.
    break <function>          Break on all overloaded functions in the current file.
    break filename:line_number
    break filename:function
    
    info breakpoints          List all information on current breakpoints.
    info b
    
    delete {breakpoint #/#s}  List without commas. Remove numbered breakpoints.
    delete                    Delete all breakpoints.
    
    clear                     Clears a breakpoint at the next instruction. 
    clear function
    clear filename:function
    clear line_number
    clear filename:line_number
    
    disable                   Disable all breakpoints.
    disable ... {function, filename, etc.}
    
    enable                    Enable all breakpoints.
    enable ... {function, filename, etc.}
    
    enable once {breakpoint-list}
    tbreak {args}             Temporary, single-use breakpoint.
    break +offset             Break <offset> lines from the executing line.
    break *address            Useful when source is not available.
    hbreak <hardware address>
    rbreak <regex>            grep-style, not perl-style
    
    break {break-args} if {condition}

Breakpoint Command Lists
------------------------

Instruct `gdb` to take specific actions when hitting a breakpoint.

    commands {break-point number}
    ...
    commands
    ...
    end

Examples:

    (gdb) commands 1
    Type commands for when breakpoint 1 is hit, one per line.
    End with a line saying just "end".
    >silent
    >printf "fibonacci was passed %d\n", n
    >continue
    >end
    
    (gdb) commands 1
    Type commands for when breakpoint 1 is hit, one per line.
    End with a line saying just "end".
    >silent
    >print_and_go "fibonacci() was passed %d\n" n
    >end

Watchpoints
-----------

A watchpoint is like a breakpoint, but rather than living at a point in the 
code it pauses execution whenever an expression changes value.

Catchpoints
-----------

Resuming Execution
------------------

Three clases of methods for resuming execution:
* next (`n` - execute w/o pause) / step (`s` - step _into_ functions)
* continue (`c` - just go until the next breakpoint)
* finish (`f` - step out) / Until (`u` - finish an executing loop)

Printing
--------

    p <var>                   Print a variable.
    p/x <var>                 Print in hex.
    p/x $pc                   Print current location in assembly dump.

Setting Variables from Within GDB
---------------------------------

    set x = 12
    set args 1 52 19 11       argv[1], argv[2], etc.

GDB's Own Variables
-------------------

Use `$1`, `$2`, ... to access history values.

Example:

    (gdb) set $i = 0 
    (gdb) p my_array[$i++]
    $1 = 12
    (gdb)                     # Just hit enter to repeat the command... 
    $2 = 5
    (gdb) 
    $3 = 8

Seg Faults and Unix Signals
---------------------------

Signals indicate exceptional conditions and are reported during
program execution to allow the OS or our code to react to a variety of
events.

    signal    raised by           impact
    ------    ---------           ------
    SIGSEV    hardware
    SIGFPE    hardware
    
    SIGTERM   OS
    SIGABRT   OS
    
    SIGUSR1   User code(?)
    SIGUSR2   User code(?)
    
    raise()   Process itself.
    
    SIGINT    ctrl-C              OS interrupts foreground process

It is possible to define custom behavior for the various signals:

    #include <signal.h>
    //...
        if ( choice  == 1 )
          signal(SIGINT, SIG_IGN);  // Ignore control-C
        else if ( choice == 2 )
          signal(SIGINT, my_sigint_handler);
        else if ( choice == 3 )
          signal(SIGINT, SIG_DFL);
        else if ( choice == 4 )
          raise(SIGSEGV);
        else
          puts("What ever you say, guv'nor.\n\n");
    //...
    void my_sigint_handler( int signum )
    {
      printf("I received signal %d (that's 'SIGINT' to you).\n", signum);
      puts("Tee Hee!  That tickles!\n");
    }

Core Dumps
----------

The dump size is typically strictly limited. To open it up:

    ulimit -c unlimied

Or

    ulimit -C n   # kB

    $ file core.14596
    core.14596: Mach-O 64-bit core x86_64

On some OSs, file will tell which program the core came from.

We can use the cores when debugging:

    cgdb myExe /cores/core.14826

GDB Threads Command Summary
---------------------------

* `info threads`
* `thread 3`              # n, change to thread n
* `break 88 thread 3`     # break when thread 3 reaches line 88
* `break 88 thread 3 if x == y`

Run the Program in a Different Terminal
---------------------------------------

1. Go to a new terminal and type "tty" to get its address (e.g., `/dev/ttys017`),
then `sleep 10000000` (so keyboard input goes to the program and not the shell).
2. Launch `gdb`, and type `tty <address>`, e.g., `tty /dev/ttys017`. This will 
direct output to that window.

To attach to a live program
---------------------------

1. Launch the program, then use ps to figure out the pID:

        ~$ ps -leaf | grep psax
          501 11628 11016     4006   0  31  0  2433232   1032 -      S+
          0 ttys019    0:00.00 ./psax            9:32AM

2. Then attach in `gdb`:

        psax$ cgdb psax
        (gdb) attach 11628
        ... etc.

Also, `(c)gdb attach 11628` would work.

TUI 
---

* While running: `ctrl-x ctrl-a`
* At launch: `gdbtui` or `gdb -tui ...`
* Switch focus: `ctrl-o`
* Refresh the screen: `ctrl-l`
