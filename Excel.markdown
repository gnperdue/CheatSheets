
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

* Select a set of rows or columns.
* Click on the "Data" tab and press the "Filter" button (under "Sort & Filter") to 
enable "auto-filtering".
* Once auto-filtering is enabled, we have drop down menus we can use to filter.
* We can disable the filtering by toggling the "Filter" button in the "Data" tab
or by just working with the filtering drop-down menus.
* Note that with the filtering drop-downs, we can also sort the set with the
filtering layer applied. For more advanced sorting, use the "Sort" button under
the "Data" tab with all the data selected. There is a small drop-down menu on "Sort",
and in that menu there is a "Custom Sort" option.

### Using PivotTables

* Select the data region (e.g., `A1:F200`).
* From the Data tab, press the `PivotTable` button and select for Excel to create a new
sheet with a pivot table.
* Typically, the table is pre-populated. It is safe to uncheck all the items in the builder
first. (You may also remove items by dragging them out the areas and "throwing them away.")
* Then, construct the table by dragging items from the `Field name` area to the `Row Labels`
and then to the `Column Labels` or `Values` areas. Click the `i` button on the item in
the `Values` areas to select an aggregation function (e.g., `Sum`, `Count`, `Average`, etc.)
* A typical approach is drag the category of "interest" to the `Row Labels` area. Then,
drag the category you would like to aggregate over to the `Values` area and select an
aggregation method. Finally, select the category you would like to use as a breakdown to
the `Column Labels` area.

### Using array formulae

* By default, Excel functions return single values. In order to get them to return an 
array (e.g., the output of the `TRANSPOSE()` function), you need to enter the calculation
with `cmd-return` rather than just `return`.
* e.g., `=SUMPRODUCT(B2:B15,TRANSPOSE('Fee Schedule'!B2:O2))` must be enterd with 
`cmd-return` or the `SUMPRODUCT()` will fail because `TRANSPOSE()` will return a 
single value.

### Using the Solver

* First, `Solver` must be added if it isn't already. Go to `Tools` then `Add-ins`
and select `Solver.xlam` from the menu. This will cause a `Solver` button to appear in
the `Analysis` section of the `Data` tab.
* Click the `Solver` button.
* Fill the `Set Objective` cell and select the `To` values for it.
* Set the range for the `Variable Cells`.
* Then, add constraints (values must remain integers, some other cell that is a sum of the
variable cells must remain fixed, etc.)
* Select a Solving Method (sublte).
* Click `Solve`.

### Removing Extraneous Punctuation

Clean up tweets with the following sequence:

* `=LOWER(A2)`
* `=SUBSTITUTE(B2, ". ", " ")`
* `=SUBSTITUTE(C2, ": ", " ")`
* `=SUBSTITUTE(D2, "?", " ")`
* `=SUBSTITUTE(E2, "!", " ")`
* `=SUBSTITUTE(F2, ";", " ")`
* `=SUBSTITUTE(G2, ",", " ")`

### Break up a string into tokens

* In the Data tab, there is a powerful `Text to Columns` button.

### Sample from the normal distribution

    =NORMINV(RAND(), MEAN, STANDARD_DEVIATION)

(Note, we use the standard deviation here and not the adjusted (N-1) deviation.)

### Other useful statistical functions

* Compute the total sum of squares (sum of the squared deviations of each value in the 
outcome sample in a linear regression from the average value of the outcome sample): 
`=DEVSQ(A1:A100)`
