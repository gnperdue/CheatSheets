
# Excel 2011 for Mac

## Sources

* "Data Smart" by John W. Foreman

### Freeze header rows

Choose "Freeze Panes" or "Freeze Top Row" from the "Layout" tab on a Mac. (It is
over on the far right, under the "Window" sub menu.)

### Quickly move around

* `Command-arrow`

### Select quickly

Many tricks:

* Select a colum (or row) and then just drag to select many.

### Copy formulae quickly

1. Click on a cell and enter a formula.
2. Drag the right-bottom corner to expand the cells computed. Alternatively, double-click
the bottom-right corner to fill a column quickly.

### Absolute references

Use a `$` in the cell coordiantes, e.g. `$c2`, `c$2`, or `$c$2` depending on your needs.

### Conditional formatting

Under the "Home" tab there is a "Conditional Formatting" menu.

### Convert forumale to values

Right click the target (cell, column, or row) and choose "Paste Special" and then select
"Values" from the menu.

### Transpose a row or column

Copy a row or column and then right click the target and choose "Paste Special" and then 
toggle the "Transpose" button.

### Charts

* Select target cells and then go to the "Charts" tab and select a chart. Sections of the
chart may be right-clicked to bring up formatting menus.

### Search and replace 

There is a search box with a drop-down menu in the upper right-hand corner of the
sheet. We may also use `Command-f` to bring up the menu.

### Find a value in a range and return its location

Use, e.g., `=MATCH( <value>, <range, e.g. a1:a10>, 0)` where the trailing `0` forces
`MATCH` to give us back the position of the value itself.

### Get a value by coordinate

* Use, e.g. `=INDEX(a1:b10, 1, 1)` to get the upper leftmost item, `=INDEX(a1:b10, 3, 2)`
to get the item in the third row, second colum of the range `a1:b10`, etc.
* Use, e.g. `=OFFSET(<location>, <+row>, <+col>)`, e.g. `=OFFSET(a1, 3, 0)` to get an
item three rows down from `a1` and in the same column.

### Get the `n`th smallest or largest

Use, e.g.,

* `=SMALL(c1:c10, 1)` for the smallest item in `c1:c10`
* `=SMALL(c1:c10, 3)` for the third smallest item in `c1:c10`
* `=LARGE(c1:c10, 2)` for the second largest item in `c1:c10`

### Find a location in a range and return its value

Use `VLOOKUP`, e.g.

* `=VLOOKUP(<value>, <table or array>, <column index>, [<range lookup>])`
* `=VLOOKUP(B2, MySheet!$A$2:$B$10, 2, FALSE)` where `2` is the relative column we
want the value retrieved from and `FALSE` means we won't accept approximate matches.

Similarly, there is an `HLOOKUP` function.

### Filtering and sorting

1. Select a set of rows or columns.
2. Click on the "Data" tab and press the "Filter" button (under "Sort & Filter") to 
enable "auto-filtering".
3. Once auto-filtering is enabled, we have drop down menus we can use to filter.
4. We can disable the filtering by toggling the "Filter" button in the "Data" tab
or by just working with the filtering drop-down menus.
5. Note that with the filtering drop-downs, we can also sort the set with the
filtering layer applied. For more advanced sorting, use the "Sort" button under
the "Data" tab with all the data selected. There is a small drop-down menu on "Sort",
and in that menu there is a "Custom Sort" option.
