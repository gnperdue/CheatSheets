Comment
-------
Go the vim way. Start by only using hjkl to move the cursor.

Help
----
    www.vimdoc.sourceforge.net

Starting Up
-----------
    vim {filename}
    vim {filename} +n       Open {filename} and position the cursor on line n.
    vim *.txt

Modes
-----
Normal
Insert
Insert-Normal (Use command, then return to Insert mode.)
Operator-Pending

Comment: Below, the dash "-" between buttons signals holding the first button, then pressing the second.

Getting Help
------------
    vimtutor
    :help

Fundamentals
------------
    .                               Repeat the last command. (Includes text insertion in insert mode.) 
    i                               Enter insert mode.
    I                               Enter insert mode at the beginning of the line.
    a                               Enter insert mode one character beyond the cursor.
    A                               Enter insert mode at the end of the line.
    Esc                             Exit insert mode.
    s                               Delete the character under the cursor and enter insert mode.
    J

Moving through text
-------------------
    h, j, k, l                      Move right, down, up, or right (real lines).
    gj, gk                          Move down or up display lines.
    0, g0                           Move to the first character of the real (, display) line.
    ^, g^                           Move to the first non-blank character of the real (, display) line.
    $, g$                           Move to the end of the real (, display) line.
    w, b                            Move to the front (, back) of the next (or current/previous) word.
    e, ge                           Move to the back of the current/next word (, previous word).
    W, B                            Move to the front (, back) of the next (or current/previous) WORD.
    E, gE                           Move to the back of the current/next WORD (, previous WORD).
    :jump                           Inspect the contents of the jump list (for <ctrl-o>, <ctrl-i>).
    <ctrl-o>                        Move back through the breadcrumbs. Will jump through buffers.
    <ctrl-i>                        Move forward through the breadcrumbs.
    <ctrl-b>, <ctrl-u>              Page Up.
    <ctrl-f>, <ctrl-d>              Page Down.
    <number>|                       Move to column <number>.

Jumps (Moving through text and files...)
----------------------------------------
Jumps: Command                  Effect
--------------                  ------
    [count]G                        Jump to line number.
    //patern<CR>/?pattern<CR>/n/N   Jump to the next (previous) occurrence of pattern.
    %                               Jump from matched brace (),{},[] to another (front-back).
    (/)                             Jump to start of previous/next sentence.
    {/}                             Jump to start of previous/next paragraph.
    H/M/L                           Jump to top/middle/bottom of screen.
    gf                              Jump to file name under the cursor.
    <ctrl-]>                        Jump to the definition of keyword under the cursor. (What!?)
    '{mark}/`{mark}                 Jump to a mark (more on this elsewhere...)
    
Modify Jump to File
-------------------
    :set suffixesadd+=.rb           Etc. Add the specified extension and vim will try to use them with gf.

Changes (Moving through them...)
--------------------------------
    :changes                        List the changes.
    g; / g,                         Traverse the change list (back / forwards).
    `.                              Jumps to the location of the last change (see more under Automatic Marks).
    `^                              Jumps to the last insertion.
    gi                              Move to last insertion point and enter insert mode.

Searching
---------
    /{pattern}                      Search forward in the buffer for {pattern}.
    ?{pattern}                      Search backwards in the buffer for pattern.
    n                               Repeat the search going "forward" (in the expected direction)..
    N                               Repeat the search with direction reversed.
    /<cr>                           Jump forward to the next match of pattern (don't preserve direction or offset).
    ?<cr>                           Jump backward to the next match of pattern (don't preserve direction or offset).
    f<char>                         Search for the next instance of character <char>.
    ;                               Repeat the last search "f" performed.
    ,                               Reverse the last character search command.
    F<char>                         Search backwards through the text for the next instance of <char>.
    t<char>                         Search forward to the next character before the next occurrence of <char>.
    T<char>                         Search backward to the character after the previous occurrence of <char>.
    *                               Place the cursor on the word you want to search for (repeats of).
    :set ignorecase                 Turn on case-insensitive search.
    \c                              Ignore case in *this* search (regardless of set setting). (Put anywhere in search term.)
    \C                              Use case in *this* search(regardless of set setting). (Put anywhere in search term.)
    :set smartcase                  Ignore case in the search by default unless we include a capital letter in the search.
    /#\([0-9a-fA-F]\{6}\)           Search for six consecutive hexadecimal numbers preceeded by a # sign. (Optionally also escape the closing }).
    /\v                             Active the "very magic search switch." (All characters assume special meaning except _, a-zA-Z0-9.
    /\v#([0-9a-fA-F]{6})            Search for six consecutive hexadecimal numbers preceeded by a # sign. 
    /\v#(\x{6}|\x{3})               Search for six or three consecutive hexadecimal numbers (w/ hex character class) preceeded by a # sign. 
    /\V                             Activate the "very nonmagic" search switch. (All characters except \ lose special meaning - literal search.)
    ?\V                             Activate the "very nonmagic" search switch. (All characters except \ and ? lose special meaning - literal search.)
    /\v<word>                       Use <> to mark the boundaries of a word (e.g., search for "the" and not "these", etc.).
    :nohlsearch                     Unlike :set nohlsearch or :set hls!, this turns of highlighting until the next search is performed. (:noh)
    <ctrl-r> <ctrl-w>               Autocomplete search field using remainder of highlighted selection (when :set incsearch is active).
    /{pattern}/e                    Position the cursor at the end of the pattern when searching (default is the beginning).
    //e                             Anchor the next search of a previous pattern to the end (no need to have /e'd initially). Can be used as a motion.
    <ctrl-r> /                      Paste the contents of the last search register in place (insert mode, command line mode).
    :let @/='Pragmatic Vim'         Set the last search register to 'Pragmatic Vim'.

Substitution
------------
    :s/{pat1}/{pat2}/               Substitute the first instance of {pat1} with {pat2} on the current line.
    :s/{pat1}/{pat2}/g              Substitute all instances of {pat1} with {pat2} in the current line.
    :[range]s/{pat1}/{pat2}/g       Substitute all instances of {pat1} with {pat2} over the specifiec range of lines.
    :33,34s/aa/ab/gc                Replace aa with ab on lines 33 and 34.
    g&                              Repeat the last substitution over the entire file.
    :%s/{pat1}/{pat2}/gc            Search and replace pat1 with pat2 and prompt each time over the whole file.
    :%s/{pat1}/<ctrl-{register}>/   Search and replace pat1 with the contents of register {register}.
    :%s/{pat1}/\=@{register}/       Use the contents of register {register}, passing the contents by value. (e.g. @0 for the yank register, @" for default)
    :%s//{string}/gc                Search and replace using the last match.
    :%s///gn                        Count the number of matches of the last search pattern used, don't do anything (n suppression).
    :&&                             Replay the last substitution over the current line.
    :%&&                            Repeat the last substitution over the entire file (longer g&).
    :'<,'>&&                        Replay the last substitution over the visually selected range (get '<,'> automatically with : from visual mode).

Special Characters in Substitution Command Replacement Strings
--------------------------------------------------------------
    Symbol                          Represents
    ------                          ----------
    \r                              Carriage return.
    \t                              Tab.
    \\                              Backslash.
    \1                              Insert the first submatch.
    \2                              Insert the second submatch (and so on, up to \9).
    \0                              Insert the entire matched pattern.
    &                               Insert the entire matched pattern.
    ~                               Use {string} from previous substitute.
    \={Vim script}                  Evaluate {Vim script} expression, use the reult as the replacement {string}.

Editing in Replace Mode
-----------------------
    R                               Enter replace mode.
    <insert>                        Also may use the insert key to enter replace mode (if present).
    gR                              Virtual replace mode (treats tab stops as though they were a single space).
    r{char}                         Replace a single character.
    gr{char}                        Replace a single character in virtual mode.
    Vr-                             Select a line and replace all the characters with "-"

Mark Text 
---------
    m{a-zA-Z}                       Lower case letters mark only the buffer, uppercase are global (across all buffers).
    '{mark}                         Jump to the line where the mark was set.
    `{mark}                         Jump to the exact point the mark was set.

Automatic Marks 
---------------
    Keystrokes                      Buffer Positions
    ----------                      ----------------
    ''                              Position before the last jump within current file.
    '.                              Location of last change (beginning of line).
    '^                              Location of last insertion (beginning of line).
    '[                              Start of last change or yank.
    ']                              End of last change or yank.
    '<                              Start of last visual selection.
    '>                              End of last visual selection.

Repeatable and Reversible Actions
---------------------------------------------------------------------------
    Intent                          Act                     Repeat      Reverse
    ------                          ---                     ------      -------
    Make a change.                  Edit                    .           u
    Scan line for next.             f{char}/t{char}         ;           ,
    Scan line for previous.         F{char}/T{char}         ;           ,
    Scan document for next.         /{pattern}<CR>          n           N
    Scan document for previous.     ?{pattern}<CR>          n           N
    Perform substituion.            :s/target/replacement   &           u
    Execute a sequence of changes.  qx{changes}q            @x          u

Run Commands in the Shell
-------------------------
    :!                          Access the shell.
    :!ls                        Run ls in the shell. (Note, :ls shows the contents of the buffer list.)
    %                           On vim's command line, this is short hand for the current filename. 
    :!ruby %                    Runs the current (ruby) file being edited.
    :shell                      Start an interactive shell session inside vim. (Use "exit" to return to vim.)
    :read !{cmd}                Put the output of cmd into the current buffer.
    :write !{cmd}               Use the current buffer as input for cmd.
    :write {file}               Write the current buffer into {file}.
    :write! {file}              Write the current buffer into {file} and overwrite the contents. Watch the ! placement!
    :[range]!{cmd}              Pass the lines in range to cmd and replace the range with the output of cmd.
    :!mkdir -p %:h              Make all the directories needed to write a file into its current path.

Working with Files
------------------
    :cd {path}                  Change vim's working directory.
    :pwd                        Show vim's present working directory.
    :edit {filename}            Open a file into the buffer for editing.
    :edit!                      Re-read the current file into the buffer and discard exisitng changes. (:e!)
    :edit %<tab>                % is a short-hand for the active buffer filepath.
    :edit %:h<tab>              The :h modifier removes the filename while preserving the rest of the path.
    :find {file}                Open a file by name without a fully qualified path. (<tab> completion is available.)
    :set path+={dir}/**         Add a directory to the vim "$PATH". (** matches all subdirectories below {dir})
    :set path?                  Inspect the value of the path.

Write Changes from a Buffer to a File
-------------------------------------
    :write                                ZZ will also write and close.
    :update
    :saveas
    :w !sudo tee % > /dev/null            Write the current buffer as the super-user. (% expands to the path of the current buffer.)

Manipulate File Buffers
-----------------------
    :ls                                   List the files.
    :bnext                                Switch to the next buffer. (:bn) 
    :bprev                                Switch to the previous buffer. (:bp)
    :bfirst                               Move to the first buffer. (:bf)
    :blast                                Move to the last buffer. (:bl)
    :buffer N                             Move to buffer N (:ls shows the buffer numbers). (:buf N)
    :buffer {buffname}                    Move to the buffer with name {buffname} (shown by :ls, no need for " characters).
    <ctrl-^>                              Toggle between the current and alternate buffers.
    :bufdo                                Run an Ex command on all the buffers.
    :bdelete N1 N2                        Delete buffers numbered N1 and N2.
    :N, M bdelete                         Delete buffers numbered N through M (this has no effect on the associated file).
    :5,10bd                               e.g, Delete buffers numbered 5 through 10.
    :args                                 List of files used to launch vim. (well, more than that actually...)
    :args {arglist}                       Populate the arguments list. (e.g., vim, followed by :args {file1} {file2}). Accepts wildcards.
    :args **/*.*                          * is a 0 or more character wildcard. So is **, but it can recurse downward into directories below.
    :args **/*.js **/*.css                Just get all the JavaScript and CSS, etc.
    :args `cat .chapters`                 Use shell expansion inside the backticks.
    :next                                 Move through the argument list.
    :prev                                 Move through the argument list.
    :argdo                                Execute the same command on every buffer in the set.
    :argdo %s//{pat1}/ge                  Substitute the last search match with {pat1} in all of "argslist" across the whole files, suppressing error messages.
    :argdo update                         Save every file, but only if it has been changed.

Managing Hidden Files
---------------------
    :ls                                                                                                                      
      1 %a + "a.txt"                        line 17   # <- "+" <- Modified.
      2      "b.txt"                        line 0
    :bn!
    :ls
      1 #h + "a.txt"                        line 17   # <- "h" <- Hidden file.
      2 %a   "b.txt"                        line 1

Working with the Filesystem
---------------------------
    vim .                                   Open a filesystem browser in the current directory.
    k,j <cr>                                Navigate vim's representation of the filesystem, open the selected file.
    :edit {path - directory name}           Open a filesystem browser in the specified directory. (always recall ":edit ." or ":e.")
    :edit %:h                               Open a filesystem browser in the directory of the current file.
    :Explore
    netrw-%                                 Create new files. (% in netrw, etc.)
    netrw-d                                 Create new directories.
    netrw-rename                            Rename a file.
    netrw-del                               Delete a file.

Split Windows
-------------
    <ctrl-w> s                              Split windows horizontally.
    <ctrl-w> v                              Split windows vertically.
    <ctrl-w> {s/v} :edit {filename}         Create a split and edit.
    :split {filename}                       Combo - create a split and edit. (Horizontal.) (:sp {file})
    :vsplit {filename}                      Combo - create a split and edit. (Vertical.) (:vsp {file})
    <ctrl-w> w                              Cycle focus between open windows. Also, <ctrl-w> <ctrl-w> (ctrl-"ww").
    <ctrl-w> h                              shift focus to the left.
    <ctrl-w> j                              shift focus below.
    <ctrl-w> k                              shift focus above.
    <ctrl-w> l                              shift focus to the right.
    :close                                  Close the active window. (:cl), Also <ctrl-w> c
    :only                                   Keep only the active window. (:on), Also <ctrl-w> o
    <ctrl-w> =                              Equalize width and height of all windows.
    <ctrl-w> _                              Maximize height of active window.
    <ctrl-w> |                              Maximize width of active window.
    [N]<ctrl-w>                             Set active window height to N rows.
    [N]<ctrl-|>                             Set active window width to N columns.
    [ Look up more details on window-moving in the help and check Vim-casts.org ]

Tabs
----
    :lcd {path}                             Set up the working directory locally for the current window.
    :windo lcd {path}                       Set up the working directory locally all windows in a tab. 
    :tabedit {filename}                     Open a tab with file {filename}. (:tabe {filename})
    <ctrl-w> T                              Move the current window into its own tab.
    :tabclose                               Close the current tab and all of its windows. (:tabc)
    :tabonly                                Keep only the current tab and all of its windows.
    [N]gt                                   Go to tab N.
    :tabnext {N}                            Switch to tab N. (:tabn {N})
    gt                                      Next tab.
    :tabnext                                Next tab. (:tabn)
    gT                                      Previous tab.
    :tabprevious                            Previous tab. (:tabp)

Switch to Normal Mode from Insert Mode
--------------------------------------
    <esc>
    <ctrl-[>

Switch to Insert-Normal Mode from Insert Mode
---------------------------------------------
    <ctrl-o>

Switch to Visual Mode
---------------------
    v                       Enable character-wise visual mode. (And return to normal mode - toggle.)
    <ctrl-g>                Enter Select Mode from visual mode.
    V                       Enter line-wise visual mode.
    <ctrl-v>                Enter block-wise visual mode.
    o                       Go to the other end of highlighted text.

Selection in Visual Mode
------------------------
    gv                      Reselect the last visual selection.
    vit                     Select inside a tag (e.g., (cursor here->)<a>select me</a>) on a line.

Using a Visual Operator
-----------------------
    vU                      Make the selection uppercase.
    vu                      Make the selection lowercase.

Delimited Text Objects (Begin and end with matching symbols.
----------------------
    v<text object>          Enter visual mode and use the following to make a selction of...
    Remember, text objects can be {motion}s.
    a) or ab                A pair of (parentheses).
    i) or ib                Inside of (parentheses).
    a} or aB                A pair of {braces}.
    i} or iB                Inside of {braces}.
    a]                      A pair of [brackets].
    i]                      Inside of [brackets].
    a>                      A pair of <angle brackets>.
    i>                      Inside of <angle brackets>.
    a'                      A pair of 'single quotes'.
    i'                      Inside of 'single quotes'.
    a"                      A pair of "double quotes".
    i"                      Inside a pair of "double quotes".
    at                      A pair of <xml>tags</xml>.
    it                      Inside a of <xml>tags</xml>.

Bounded Text Objects (Defined by boundaries.)
--------------------
    Remember, text objects can be {motion}s.
    iw                      Current word.
    aw                      Current word plus one space.
    iW                      Current WORD.
    aW                      Current WORD plus one space.
    is                      Current sentence.
    as                      Current sentence plus one space.
    ip                      Current paragraph.
    ap                      Current paragraph plus one blank line.

Command Line Mode
-----------------
    :                       Enter the Ex Command mode.
    /                       Enter the pattern search mode.
    <ctrl-r> <ctrl-w>       Insert the word under the cursor.
    *                       /\<<ctrl-r> <ctrl-w>\><cr>
    /<ctrl-r> <ctrl-w>       Search for the word under the cursor.

Command Line Window
-------------------
    q:                      Bring up the window with a history of the Ex commands.
    k, j                    Scroll through the command line window.
    <cr>                    Execute the contents of the current line.
    q/                      Bring up the window with a history of searches.
    <ctrl-f>                Switch from the command line mode to the command line window.

Operators
---------
    >                       Shift (the line?) right.
    <                       Shift (the line?) left.
    gUit                    Select text inside a tag and shift it to uppercase (tip 23).

Indentation
-----------
    >                       Indent the line (or visually selected text).
    2>                      Indent the line twice (3> for three times, etc.).
    >G                      Increase indentation from here to the end of the file.
    =G                      Autoindet from here to the end of the file.
    ==                      Indent current line.

Editing
-------
    s                       Remove the character under the cursor and enter insert mode.
    c{motion}               Remove text and enter insert mode. $, l, w
    ciw                     Remove the current word and enter insert mode.
    u                       Undo the last change.
    U                       Undo all changes to the line.
    <ctrl-r>                Re-do the last undo.
    daw                     Delete a word (cursor may be located anywhere within the word).
    dap                     Delete a paragraph.
    d{motion}               Delete. (Power move, especially with / search.)
    ~                       Toggle case of the character under the cursor or all visually selected text.
    g~                      Swap case. (requires motion?)
    gu                      Make lower case. (requires motion?) guaw = convert a word, guap = paragraph 
    gU                      Make upper case. (requires motion?) gUaw = CONVERT a word, gUap = paragraph, gUgU converts a line.

Deleting (c instead of d to enter insert after the edit).
--------
    dh / x                  Delete one character backwards.
    dl / X                  Delete one character forwards.
    db                      Delete one word backwards.
    dw                      Delete one word forwards.
    dB                      Delete one non-blank word backwards.
    dW                      Delete one non-blank word forwards.
    d$ / D                  Delete to the end of the line.
    d0                      Delete to the beginning of the line.
    0d$ / dd                Delete the line.

Editing In Insert Mode
----------------------
    <ctrl-h>                Delete back one character.
    <ctrl-w>                Delete back one word.
    <ctrl-u>                Delete back to the start of the line.
    <ctrl-r> N              Paste from register N. (Press and hold ctrl-r, then release, then press the number.)
    <ctrl-r> <ctrl-p> N     Smarter paste from register N.
    <ctrl-v> Code           Enter a unicode character (expect 3 digits).
    <ctrl-v> u{Code}        Enter an arbitrary code (e.g., u00bf = ¿).
    <ctrl-v> {nondigit}     Enter a nondigit literally (e.g., a literal tab instead of spaces in case exapandtab is active).
    <ctrl-k> {char1}{char2} Enter a unicode character via digraph, e.g. <ctrl-k> ?I = ¿. View a list of digraphs with :digraphs

Using the Expression Register
-----------------------------
    <ctrl-r> =              In insert mode.

Copying, Cutting, and Pasting (Yanking, Deleting, and Putting)
-------------------------------------------------------------
    Regisers are [a..z] for overwriting and [A..Z] for appending.
    The system clipboard is "+ (X11 at least).
    "{register}             Prefix to specify the register for holding the yank/delete. Defaults to unnamed ("). 
    :reg                    Examine the contents of the registers.
    :reg "0                 Examine the contents of the yank register. (Also shows the contents of "" (unnamed).)
    y{motion}               Copy (? ... $, l, w) into the unnamed register. Also copy into the yank register ("0)!
    yiw                     Copy a word.
    yi[                     Copy everything inside the [] braces (cursor should be inside the []).
    yy                      Copy a line.
    yyp                     Copy a line and put it (immediately below the current line).
    yt,                     Copy to the next comma.
    y$                      Copy to the end of the line.
    p                       Paste (removed with x, copied with y, for example) after the cursor position.
    P                       Paste (removed with x, copied with y, for example) before the cursor position.
    puP / Pup               Paste the other way when you get it wrong...
    ""p                     Paste from the unnamed register (""p == p).
    "ap                     Paste from register a.
    "0p                     Paste from the yank register (may also be equivalent to the unnamed or another register).
    xp                      Cut and paste a character - effectively transpose two characters.  
    diw                     Cut a word.
    dd                      Cut a line.
    ddp                     Cut and paste a line (one below the current line) - effectively transpose two lines.
    v{selection}p           Swap the highlighted portion in visual mode with the contents of (the unnamed) register, and vice versa.
    "{register}v{sel}p      Swap the highlighted portion in visual mode with the contents of the register, and vice versa.
    <ctrl-r>{register}      Insert Mode: Paste from register {register}. (Recall <ctrl-r"> to get the unnamed!) Useful with Ex commands too!

Default Registers
-----------------
    "=                      Expression Register
    "%                      Name of current file.
    "#                      Name of alternate file.
    ".                      Last inserted text.
    ":                      Last Ex command.
    "/                      Last search pattern (can be set explicitly with :let ).

Addition
--------
    N <ctrl-a>                                      Add N to the next number on the line, e.g. 10 -> 20
    N <ctrl-x>                                      Subtract N from the next number on the line, e.g., 30 -> 20 

Compound Commands
-----------------
    A           $a
    C           c$
    s           cl
    S           ^C
    I           ^i
    o           A<CR>                               # Leverage undo power by finishing lines with {stop} <esc> o
    O           ko

Screen Redraw
-------------
    zz                                              Redraw the screen with the cursor position in the vertical center of the page.
    z.                                              Redraw the screen with the cursor position in the vertical center of the page.
    zt                                              Redraw the screen with the cursor position at the top of the page.
    <ctrl-l>                                        Clear and redraw the screen. 

Ex Commands
-----------
    <ctrl-d>                                        Offer autocompletion suggestions. Tab to cycle through them.
    :colorscheme <ctrl-d>                           Show all the colorscheme options (tab to cycle through).
    :help ex-cmd-index                              See the ex-cmd-index for the full list of commands.
    :{N}                                            Jump to line N.
    :$                                              Go to the end of the file.
    :print                                          Print the line. (Abbreviate with :p)
    :2,5p                                           Print lines 2 to 5. (.,$p prints from the current line to EOF).
    :%p                                             Print all the lines in the file.
    :/{pattern1}/+1,/{pattern2}/-1p                 Print all lines between, but not including, those matching patterns 1 & 2.
    :[range]delete[x]                               Delete specified lines into register x. (e.g., :3d deletes line 3).
    :[range]yank[x]                                 Yank specified lines into register x.
    :[line]put[x]                                   Put the text from reigster x after the specified line.
    :[range]copy{address}                           Copy the specified lines to below the line specified by {address}. 
    :6copy.                                         Copy line 6 to below the current line.
    :6t.                                            Copy line 6 to below the current line. ( t == copy )
    :t.                                             Duplicate the current line without using a register (yyp uses a register).
    :[range]move{address}                           Move the specified lines to below the line specified by {address}. ( abbrev m )
    :[range]join                                    Join the specified lines.
    :[range]normal{commands}                        Execute normal mode {commands} on each specified line.
    :[range]substitute/{pattern}/{string}/[flags]   Replace {pattern} with {string} on the specified lines. (:[range]s/{pattern}/{string}/[flags])
    :%s/{pattern}/{string}/[flags]                  Do the substitution over the entire file, looking for pattern, etc.
    :%s/{pattern}/{string}/[flags={g,c,n,&}]        Flags: g=global (all in a line), c=confirm, n=no subs, report number, &=reuse flags from last "s"
    :[range]global/{pattern}/[cmd]                  Execute Ex [cmd] on all specified lines with a {pattern} match.
    :qall!                                          Quit and discard all unsaved changes in all open buffers.
    :wall                                           Write all modified buffers to disk. (:wa)
    :write
    :wnext                                          Write, followed by "next."
    :tabnew
    :split
    :prev/:next
    :bprev/:bnext
    @:                                              Repeat the last Ex command.
    :normal <cmd>                                   For each selected line, execute the normal mode command <cmd>. (jVG :normal .)
    :%normal A;                                     Select all modes and run normal "A;" (append a semicolon to every line).
    :%normal i//                                    Comment out every line (.js or .cpp).                                  
    :delete {register}                              Cut the current line into {register} 
    :yank {register}                                Copy the current line into {register} 
    :put {register}                                 Put the line from {register} 
    :edit!                                          Undo all changes (back to last save?).
    :sort                                           Sort!

Global Commands
---------------
    :[range]global[!]/{pattern}/[cmd]               Execute an Ex command on each line that matches a pattern.
    :[range]global[!]/{pattern}/[range][cmd]        Template is expandable...
    :g/re/p                                         Print a regular expression globally. ^_^
    :g/re/d                                         Delete all lines matching a regular expression globally. 
    :[range] vglobal /{pattern}/ [cmd]              Execute an Ex command on each line that doesn't match a pattern.
    :v/re/d                                         Delete all lines NOT matching a regular expression globally. 
    :g/TODO/yank A                                  Copy all lines with TODO in them into register a (use upper case to append).
    :g/{/ .+1,/}/-1 sort                            Sort all items between all braces {} in a bufer.

Macros
------
    q{register}                                     Start recording a macro to {register} (e.g. "q"). Lower-case to overwrite, upper case to append.
    qq                                              Start recording into register q.
    q                                               Stop recording.
    qQ                                              Append additional commands to the macro in register "q".
    q                                               Stop appending.
    :reg {register}                                 Examine the macro in {register}. (Useful before appending.)
    @{register}                                     Execute the macro in {register}.
    @@                                              Execute the most recently *invoked* {register}.
    N@{register}                                    Execute the macro in {register} N times.
    :normal @{register}                             Apply the macro to every visually selected line of text (e.g. vG:normal @a)
    :argdo normal @{register}                       Apply the macro to all open buffers. (Often lead with :edit! to undo file where we recorded the macro.)

Vim Script
----------
    :let i=0                                        Assign 0 to i.
    :echo i                                         Print i (not to the buffer).
    :let i += 1                                     Increment i.
    <ctrl-r> =i<cr>                                 Insert i into the buffer.
    :let @a=substitute(@a, '\~', 'vU', 'g')         Substitute text *inside* the register.

Tags
----
    <ctrl-]>                                        Jump to a definition.
    <ctrl-t>                                        Jump back through the tag history.
    g<ctrl-]>                                       See a list of definitions to jump to. (Then, number and <CR>.)
    :tselect                                        Show the list of definitions to jump to again (need to <ctrl-]> first).
    :tnext                                          Jump to the next match without showing a prompt.
    :tprev, :tfirst, :tlast                         Jump to matches without a prompt.
    :tag {keyword}                                  Acts like <ctrl-]>. {keyword} features tab completion.
    :tjump {keyword}                                Acts like g<ctrl-]>.
    :pop                                            Acts like <ctrl-t>.

Quickfix List
-------------
    :make                                           Run make in the shell where the buffer is.
    :cnext                                          Jump to the next error from a make (next item in the Quickfix list).
    :cprev, :cfirst, :clast                         Jump to an item in the Quickfix list.
    :cnfile, :cpfile                                Jump to the first item in the next (previous) file.
    :cc N                                           Jump to the nth item.
    :copen, :cclose                                 Open/Close the Quickfix window.
    :5cnext, :3cprev                                Jump with a count for the number of items.
    :colder                                         Look at an older version of the Quickfix list (vim stores up to 10).
    :cnewer                                         Look at a newer version of the Quickfix list.
    :setlocal makeprg=gmake\ acquire_data-lib    
    :setlocal makeprg=cmt\ make    
    :setglobal errorformat?                         Check the error format put into the Quickfix list. - %f=filename, %l=line, %m=message
    :setlocal efm={format}                          Set the format to handle errors vim doesn't know well.
    :compiler cmt make                              Activte the compiler plugin (set makeprg and errorformat).
    :args $VIMRUNTIME/compiler/*.vim                Look at the compiler plugins distributed with vim.

Location List
-------------
    :lnext, :lprev, ...

Grepping Externally
-------------------
    :grep {pattern} *                               Populate the Quickfix list with the search results (-n flag is automatically present).
    :grepprg="grep -n $* /dev/null"                 Set what :grep triggers in the external shell. (For example, call ack.)
    :grepformat="%f:%l:%m,%f:%l%m,%f %l%m"          Format the search results from the external grep triggered by :grep. (See errorformat for more.)
    :vimgrep/{pattern}/[g][j] {file}                Use vim's built-in search engine (vim regex syntax). {File} cannot be blank. (* for any file in the directory.)
    :vimgrep/{pattern}/**                           Search through all files in subdirectories recursvely. Navigate in quickfix (use :copen).
    :vimgrep/{<ctrl-r>/}/**                         Paste the last search from the search register into the pattern for external searching.

Autocompletion
--------------
    <ctrl-p> / <ctrl-n>                             From insert mode, to select the "previous" and "next" items.

Autocompletion Method Table
---------------------------
    <ctrl-n>                                        Generic keywords (built from a partial word list using a document scan).
    <ctrl-x><ctrl-n>                                Current buffer keywords.
    <ctrl-x><ctrl-i>                                Included file keywords (e.g., #include (c,c++), import (ruby, python), etc.) (Tweak the 'include' setting.)
    <ctrl-x><ctrl-]>                                Included file keywords.
    <ctrl-x><ctrl-]>                                Tags file keywords.
    <ctrl-x><ctrl-k>                                Dictionary lookup - dictionary must be populated (best with :set spell).
    <ctrl-x><ctrl-l>                                Whole line completion (duplicate an existing line from elsewhere in the buffer - use a few chars to start).
    <ctrl-x><ctrl-f>                                Filename completion (uses :pwd, so :cd {path} to get a different set).
    <ctrl-x><ctrl-o>                                Omni completion (we need a plug-in for the language we're using, see compl-omni-filetypes).

Autocompletion Pop-up Menu
---------------------------
    <ctrl-n>                                        Use the next match from the list.
    <ctrl-p>                                        Use the previous match from the list.
    <down>                                          Select the next match from the word list.
    <up>                                            Select the previous match from the word list.
    <ctrl-y>                                        Adopt the currently selected match.
    <ctrl-e>                                        Revert to the originally typed text.
    <ctrl-h> (and <BS>)                             Delete one character from the current match.
    <ctrl-l>                                        Add one character from the current match.
    {char}                                          Stop completion and insert {char}.

Autocompletion Source Material
------------------------------
    :ls!                                            Look at the keywords in the buffer list. (???)
    :set include?                                   Inspect included (e.g. header) files.
    :set complete                                   Look at the list of "locations" included in the complete commands.
    :set complete+=k                                Etc. See 'complete' documentation for the include lists and defaults.

Spelling
--------
    :set spell / :set nospell                       Show/hide spell checks.
    [s / ]s                                         Skip back / forward through misspelled words.
    z=                                              Show suggested spelling replacements.
    zg                                              Add current word to spell file.
    zw                                              Remove the current word from the spell file.
    zug                                             Revert either zg or zw commands for the current word.
    :set spelllang=en_us                            Also, en_au, en_ca, en_gb, en_nz (try =fr, will prompt for download, etc.)
    <ctrl-x>s                                       Fix spelling from insert mode (:set spell must already be active).

Programming
-----------
    shift-k                                         Open man page for word under the cursor.

Recipes - Find & Replace Across Many Files
------------------------------------------
1. Fully populate the args list (all files).    `:args **/*.txt`
2. Enable navigation w/o saving.                `:set hidden`
3. Set the search pattern.                      `/Pragmatic\ze Vim`
4. Replace with error suppression.              `:argdo %s//Practical/ge`

Recipes - Clear a Register
--------------------------
1. Start and finish a macro with no steps.      `qaq`
2. Check the register (here - a).               `:reg a`

Recipes - Sort a List
---------------------
1. Select the block of items.                   `v{motion}`
2. Apply the sort (: brings up '<,'>)           `:sort`

Recipes - Use Tags
------------------
1. Check to see tags options.                   `:set tags?`
2. Generate a tags file locally.                `:!ctags -R`
3. Ignore some noise... (etc.)                  `:!ctags -R --exclude=.git`
4. Shortcut to regenerate file.                 `:nnoremap <f5> :!ctags -R<CR>`
5. Set autocommand on save.                     `:autocmd BufWritePost * call system("ctags -R")`

Recipes - Use ack instead of grep for :grep
-------------------------------------------
1. Set a different :grepprg                     `:set grepprg=ack\ --nogroup\ --column\ $*`     # May need ack-5.12 on my Mac...
2. Set the format.                              `:set grepformat=%f:%l:%c:%m`                   # %c to go to the column!

Recipes - Add a "local" Dictionary for Project Jargon Spellings
---------------------------------------------------------------
1. Turn on spell checking.                      `:set spell`
2. Set a base language (if needed).             `:setlocal spelllang=en_us`
3. Set a local spellfile path.                  `:setlocal spellfile=~/.vim/spell/en.utf-8.add`
4. Set a local spellfile addition.              `:setlocal spellfile+=~/mydir/mysubdir/myfile.utf-8.add`
5. Add to the second spell file.                `:2zg`
6. Add to the original spell file.              `:1zg`

Recipes - Change Vim on the Fly
-------------------------------
    :set ignorecase / :set noignorecase / :set ignorecase! (toggle) / :set ignorecase? / :set ignorecase& (restore default)
    :set tabstop=2 (:set ts=2)
    :set softtabstop=2 (:set sts=2)
    :set shiftwidth=2 (:set sw=2)
    :set expandtab (:set et)
    :set ts=2 sts=2 sw=2 et
    :bufdo setlocal ts=4
    :windo setlocal number

Recipes - Customize with .vim Files
-----------------------------------
1. Name the file.                               `vim ~/mysettings.vim`
2. Source it.                                   `:source ~/mysettings.vim`
3. Syntax is the same as the .vimrc file.
    set tabstop=2
    set softtabstop=2
    set shiftwidth=2
    set expandtab

Recipes - Filetype Specific Customization
-----------------------------------------
1. Edit customizations file (e.g., ~/.vimrc):
    if has("autocmd")
      filetype on
      autocmd FileType ruby setlocal ts=2 sts=2 sw=2 et
      autocmd FileType javascript setlocal ts=4 sts=4 sw=4 noet
      autocmd FileType javascript compiler nodelint
    endif
2. Cleaner if we use the ftplugin:
    ~/.vim/after/ftplugin/javascript.vim
    setlocal ts=4 sts=4 sw=4 noet
    compiler nodelint

Reciples - Change Encoding (e.g. fix Excel exports to csv)
----------------------------------------------------------
See: http://stackoverflow.com/questions/64860/best-way-to-convert-text-files-between-character-sets

    $ file Consumer_Complaints_short.csv
    Consumer_Complaints_short.csv: Non-ISO extended-ASCII English text
    $ vim +"set nobomb | set fenc=utf8 |x" Consumer_Complaints_short.csv
    $ file Consumer_Complaints_short.csv
    Consumer_Complaints_short.csv: UTF-8 Unicode English text

Recipes - search for special characters
---------------------------------------
For example, the "new feed" charcter is "^L", this can be searched for with:

    /<ctrl-v><ctrl-l>
