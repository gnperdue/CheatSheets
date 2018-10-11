
## Fundamental

* `cmd shift p` - Open the command palette (`esc` to clear).
* `cmd shift n` - Open a new window.
* `cmd z` - Undo

## Moving

* `alt b` | `alt <left>` / `alt f` | `alt <right>`- Beginning / end of word
* `cmd <left>` | `ctrl a`- Move to first character of current line
* `cmd <right>` | `ctrl e`- Move to end of current line
* `cmd <up>` / `cmd <down>`- Move to top / bottom of file
* `ctrl g`- Move to a specific line
* `cmd r`- Bring up a list of symbols in the file (fuzzy filterable).
* `cmd f2`, `f2`- Bookmark, jump to next bookmark (_need to remap these_).

## Selections

* `shift <up>` / `ctrl shift p`, `cmd shift <up>` - Select up, select to top.
* `shift <down>` / `ctrl shift n`, `cmd shift <down>` - Select down, select to
bottom.
* `shift <left>` / `ctrl shift b`, `ctrl shift a` - Select left, select to
beginning of line.
* `shift <right>` / `ctrl shift f`, `ctrl shift e` - Select left, select to
beginning of line.
* `alt shift <left>` / `alt shift b` - Select to beginning of word.
* `alt shift <right>` / `alt shift f` - Select to end of word.
* `cmd shift <up>`, `cmd shift <down>` - Select to top, bottom of file.
* `cmd a` - Select all contents of file.
* `cmd l` - Select entire line.
* `ctrl shift w` - Select current word.

## Move and selection philosophy and principles

* `<left>` and `<right>` to move left and right.
    * Add `alt` modifier to move whole words.
    * Add `cmd` modifier to move to the beginning / end.
    * Add `shift` for selection.
* `<up>` and `<down>` to move up and down lines.
    * Add `cmd` modifier to move to the very top or bottom.
    * Add `shift` for selection.

## Editing and deleting text

* `cmd j` - Join the next line to the end of the current line.
* `cmd ctrl <up>`, `cmd ctrl <down>` - Move the current line up or down.
* `cmd shift d` - Duplicate the current line.
* `cmd k <+> cmd u` - Uppercase the current word.
* `cmd k <+> cmd l` - Lowercase the current word.
* `ctrl t` - Transpose characters on either side of cursor.
* `ctrl shift k` - Delete (the entire) current line.
* `ctrk k` - Cut to end of line.
* `cmd delete` - Cut to end of line.
* `cmd backspace` - Cut to beginning of line.
* `alt h` - Delete to beginning of word.
* `alt d` - Delete to end of word.

## Multiple cursors and selections

* `cmd click` - Add a new cursor at the clicked location. (? doesn't appear to
work...)
* `ctrl shift <up>/<down>` - Add another cursor above/below the current cursor.
(`<esc>` seems to break out.)
* `cmd d` - Select the next word in the document that is the same as the
currently selected word.
* `cmd ctrl g` - Select all the words in a document that are the same as the
current word.
* `cmd shift l` - Convert a multiline selection into multiple cursors.

## Brackets

* `ctrl m` - Jump to the matching bracket - [], (), {}. Or jump to the first
overall bracket (while between brackets).
* `cmd ctrl m` - Select the text within the current brackets.
* `alt cmd .` - Close the current XML/HTML tag.

## Find and Replace

Atom uses JavaScript's regex syntax.

* `cmd f` - Search within the current buffer (`esc` to break out).
* `cmd shift f` - Search within the entire project (`esc` to break out). Note
that we may use glob patterns in the file/directory box.

## Snippets

Use `tab` expansion for snippets. The `language-x` packages specify
language-specific snippets. We may check available snippets through the
menu and add them to `~/.atom/snippets.cson`.

* `shift cmd p` - Command palette: view "snippets: available"

## Autocomplete

* `tab` or `enter` - Use `tab`.

## Folding

* `alt cmd [` and `alt cmd ]` - Fold and unfold.
* `alt cmd shift [` and `alt cmd shift ]` - Fold and unfold everything.

## Panes

* `cmd w` - Close a pane.
* `cmd k` + `<up>` - Split a pane upwards (two separate sets of keystrokes).
* `cmd k` + `<down>` - Split a pane downwards.
* `cmd k` + `<left>` - Split a pane leftwards.
* `cmd k` + `<right>` - Split a pane rightwards.
* `cmd k` + `cmd <up>` - Move to the upper pane.
* `cmd k` + `cmd <down>` - Move to the lower pane.
* `cmd k` + `cmd <left>` - Move to the left pane.
* `cmd k` + `cmd <right>` - Move to the right pane.

## Pending Pane Items

* Single click in the tree view for a file preview.

## Grammar

...

```
this is a test, this is only a test, if this were not a test we'd be dead

[this] (is) {a} <test>
[this] (is) {a} <test>
[this] (is) {a} <test>

'the' "quick" `brown` _fox_ *jumped* /over/ THE lazy dog
'the' "quick" `brown` _fox_ *jumped* /over/ THE lazy dog
'the' "quick" `brown` _fox_ *jumped* /over/ THE lazy dog
'the' "quick" `brown` _fox_ *jumped* /over/ THE lazy dog

the quick brown fox jumped over the lazy dog
the quick brown fox jumped over the lazy dog
the quick brown fox jumped over the lazy dog
the quick brown fox jumped over the lazy dog
```
