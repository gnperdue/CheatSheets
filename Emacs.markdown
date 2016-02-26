Sources
-------

* O'Reilly Learning GNU Emacs
* http://ergoemacs.org/emacs/emacs.html


Modes (One Major Mode at a Time)
--------------------------------
Fundamental, Text, View, Shell, Outline, Indented Text, Paragraph, Picture,
HTML, SGML, LaTeX, Compilation, cc, Java, Perl, SQL, Emacs Lisp, Lisp,
Lisp Interaction

    C-h m                Check major mode

Minor Modes
-----------
Many!

Toolbar
-------

    M-<backtick>            Access the toolbar (C-g or ESC-ESC-ESC to get out)

Meta
----

    M-<n> <command>         Repeat <command> n times.
    C-u <n>                 Repeat the next command entered n times.

Help
----

    C-h ?                   List of options.
    C-h t                   Tutorial.
    C-h k                   "Describe key," e.g. C-h k C-x i
    C-h f                   "Describe function," e.g. C-h f find-file
    M-x describe-mode       See active minor modes

Saving
------

    C-x C-s
    C-x C-w                 Save as. (write-file)

Quitting
--------

    C-g                     Quit out of minibuffers, etc.
    C-x k *buffname*        Kill buffer *buffname* (default to current)
    C-x C-c                 Close emacs.

Menus
-----

    M-backtick              Access the pop-up menu. `C-g` to escape.

Open
----

    C-x C-f                 Open a file. (Supports tab completion.)
    C-x C-v                 Open an alternate file to the one just opened.

Insertion and Appending
-----------------------

    C-x i                   Insert one file into another.
    M-> C-x i               Move to the end of the file and append another one.

Moving Through Text
-------------------

    C-v                     Page down.
    M-v                     Page up.
    M->                     Move to the end of the file (M-shift-.).
    M-<                     Move to the beginning of the file (M-shift-,).
    C-a / C-e               Beginning / End of line.
    C-b/C-p/C-f/C-n         Move one char back/previous-line/char forward/next-line.
    M-f / M-b               Move one word forward/backward.
    M-a / M-e               Move back / forward one sentence.
    M-{ / M-}               Move back / forward one paragraph.
    C-x [ / C-x ]           Move back / forward one *page break*.
    C-q C-l                 Insert a page break.
    M-x goto-line           Go to line (fill in prompt).
    M-g g                   Go to line (fill in prompt).
    M-x goto-char           Go to the nth char in the file.

Move the Page
-------------

    C-l                     Re-center the page.
    C-l C-l                 Move page so cursor sits at the top.
    C-l C-l C-l             Move page so cursor sits at the bottom.
    C-l C-l C-l C-l         Move page so cursor sits in the center, etc.

Switch Buffers
--------------

    C-x o                   Cycle through buffers in a split window.
    C-x <left>              Cycle through buffers.
    C-x <right>             Cycle through buffers.
    C-x C-b                 List buffers.
    C-x 1                   Close all split windows but the active one.
    C-x 2                   Split frame above and below
    C-x 3                   Split frame left and right
    C-x 0                   Delete current window

Undo
----

    C-_ / C-x u             Undo.
    <cursor> C-x u          Re-do (of sorts).
    M-x revert-buffer       Go back to last save.
    M-x recover-file        Restore an auto-save file.

Fill Mode
---------

    M-x auto-fill-mode      Enter/Exit Fill Mode.
    M-q /                   Auto-reformat paragraphs.
    M-x fill-paragraph

Delete Kill/Erase Text (kill ring / no kill ring)
-------------------------------------------------

    C-k                     Kill to the end of the line.
    M-k                     Kill to the end of the next sentence.
    M-d                     Kill the next word.
    M-delete                Kill the previous word.
    C-x delete              Kill the previous sentence.
    C-d                     Erase the character under the cursor. (no ring)
    C-delete                Erase the previous character. (no kill ring)
    delete                  Erase the previous character. (no kill ring)
    C-w                     Kill region.
    kill-paragraph          Delete next paragraph (long binding only).
    backward-kill-paragraph Delete the previous paragraph (long only).
    M "-" -C-k               Meta -hyphen- C-k. Delete back to the line start.

Copy
----

    M-w                     kill-ring-save a region.

Comment
-------

    M-;          Comment/uncomment selected region
    C-c /        Un/Comment a line (using *my* .emacs)

Paste
-----

    C-y                     Bring a entry back from the kill ring.
    M-y                     After C-y, brings back the second-most recent
                            deletion.
    M-y                     After C-y, M-y, brings back the third-most
                            recent deletion, etc. Eventually we loop back
                            around to the first item in the ring.

Selecting Text
--------------

    C-x h                   Select all.
    C-<space> or C-@        Start the selection of a region.
    C-x C-x                 Exchange point and mark (go to beginning of
                            marked region).
    M-h                     Mark a paragraph.
    C-x C-p                 Mark the current page (defined with C-l
                            chars).

Inserting Text
--------------

    C-o                     Insert a line above the current line.

Autoindent
----------

    C-M-\                   Indent selected region.


Transposition
-------------

    C-t                       Transpose two characters.
    M-t                       Transpose two words (but not punctuation).
    C-x C-t                   Transpose two lines.
    M-x transpose-sentences   Transpose two sentences.
    M-x transpose-paragraphs  Transpose two paragraphs.


Changing Capitalization
-----------------------

    M-l                     Convert following word to lower-case
    M-l (meta-ell)          Make an entire word (after cursor) lower case.
    M-c                     Capitalize the the first letter of a word.
    M-u                     Make an entire word (after cursor) upper case.
    M- "-" (meta hyphen)    Prefix to above to fix previous word.
    C-x C-l                 Convert region to lower case
    C-x C-u                 Convert region to upper case

Overwrite Mode
--------------

    M-x overwrite-mode      Enter overwrite mode. ("M-x ov")

Searching
---------

    C-s                     Incremental. C-s repeat; enter end; C-g cancel.
    C-r                     Search backwards (C-s "backwards").
    C-s C-w                 Copy next word into the search buffer.
    C-s C-y                 Copy the rest of the line into the search.
    C-s M-y                 Copy text from the kill ring into the search.
                            (M-p, M-n to move back, forward in the ring.)
    C-s C-s                 Repeat the previous search.
    C-r C-r                 Repeat the previous backwards search.
    C-s <enter>             Simple search. C-s repeat.
    C-r <enter>             Simple backwards search. C-r repeat.
    C-s <enter> C-w         Word search (word-search-forward).
    C-r <enter> C-w         Backward Word search.

Search and Replace
------------------

    M-x replace-string      Replace a string everywhere (forward cursor).
    M-%                     Query-replace.
    C-r                     Recursive edit while a query-replace is on-going.
    C-M-c                   Exit the recursive edit; return to query-replace.
    C-]                     Abort recursive edit and query-replace.
    M-x top-level           Abort recursive edit and query-replace.

Rename
------

    M-x rename-buffer       Rename a buffer
    M-x rename-file         Rename a file

Regular Expressions in Search and Replace
-----------------------------------------

    ^                       Match the beginning of a line.
    $                       Match the end of a line.
    .                       Match any single character
    .*                      Match any group of zero or more characters.
    \<                      Match the beginning of a word.
    \>                      Match the end of a word.
    []                      Match any character in [] (e.g.[a-z])
    \s                      Match any whitespace character.
    \S                      Match any non-whitespace character.
    \d                      Match any single digit 0-9.
    \D                      Match any character but a digit.
    \w                      Match any word character.
    \W                      Match any non-word character.


Change Variables
----------------

    M-x set-variable        e.g., case-replace -> nil
                            e.g., case-fold-search -> t / f
                            (Change lasts until end of session.)
                            For permanent:
                            (setq-default case-fold-search nil) ; init.el

Repeating Complex Commands
--------------------------

    C-x <esc> <esc>         Repeat command. M-n, M-p to cycle through history.
    M-n <command>           Repeat a command `n` times. (SORT OF DOESN'T WORK)
    C-u n <command>         Repeat a command `n` times.


Formatting
----------

    M-x refill-mode                  Minor mode where paragraphs are kept "neat"
    M-x auto-fill-mode               Use M-q to format edited paragraphs
    M-x set-fill-column              Set the outer edge for editing fill mode
    M-x paragraph-indent-text-mode
    M-x fill-region                  Highlight the area first
    M-x delete-trailing-whitespace

Keyboard Macros
---------------

    C-x (                 (or f3) Start defining a macro
    C-x )                 (or f4) Finish the macro definition
    C-x e                 (or f4) Execute the keyboard macro
    C-u 10 C-x e          Execute the keyboard macro 10 times
    C-u 0 C-x e           Execute the macro infinitely (to EOF)
    M-x apply-macro-to-region-lines

Colors
------

    M-x list-colors-display     List available colors

Interact with the Shell
-----------------------

    M-x shell     Launch a shell (then `ipython`, etc.)

Very Important Commands
-----------------------

    C-f             Move forward a character
    C-b             Move backward a character

    M-f             Move forward a word
    M-b             Move backward a word

    C-n             Move to next line
    C-p             Move to previous line

    C-a             Move to beginning of line
    C-e             Move to end of line

    M-a             Move back to beginning of sentence
    M-e             Move forward to end of sentence

    <DEL>           Delete the character just before the cursor
    C-d             Delete the next character after the cursor

    M-<DEL>         Kill the word immediately before the cursor
    M-d             Kill the next word after the cursor

    C-k             Kill from the cursor position to end of line
    M-k             Kill to the end of the current sentence

    C-x C-f         Find file
    C-x C-s         Save file
    C-x s           Save some buffers
    C-x C-b         List buffers
    C-x b           Switch buffer
    C-x C-c         Quit Emacs
    C-x 1           Delete all but one window
    C-x u           Undo

    M-q             Trim all selected, wrapped lines.

    C-g             Cancel a command before it is finished being typed.

Special Packages: Ido
---------------------

    C-x b      ido-switch-buffer

Inside `ido-switch-buffer`:

    C-f        Stop suggestion (make a new file) (at end of name, may need 2x)

