# SVN

### Help

    svn help
    svn help <command>


### Imports

    svn import /path/to/mytree \
      http://svn.example.com/svn/repo/some/project \
      -m "Intitial import"


### Check Out

    svn checkout <url>
    svn checkout http://svn.example/com/svn/repo/trunk
    svn checkout http://svn.example/com/svn/repo/trunk/src    # go deeper


### Commits

    svn commit <file> -m "message"
    svn commit -m "message"   # if you don't provde -m or -F, get a window to edit...
    svn commit -F logmsg           


### Updates and Conflict Resolution

    svn update                     # provides a menu to handle conflicts
    svn update --non-interactive   # always postpone conflict resolution
    svn update -r <rev #>                    # go ``back in time'' to rev #
    svn resolve
    svn resolve --accept working <file>      # must list the files to be resolved
    svn resolve --accept theirs-full <file>  # discard local edits
    svn revert <file>                        # no need for `resolve`


### Status 

    svn status --verbose    # Also, `svn status FOO`. Opts: `-u -v`
    svn status -u           # check for conflicts


### Examining History

    svn diff
    svn diff > patchfile    # See also `svn patch`
    svn diff --diff-cmd /usr/bin/diff -x "-i" foo.c   # Use a different `diff` engine. 
    svn diff -r <rev #> <file>
    svn diff -r <rev #1>:<rev #2> <file>
    svn diff -c <rev #> <file>            # compare a revision to the previous revision
    svn diff -c 5 http://svn.example.com/repos/example/trunk/text/rules.txt
    svn log
    svn log -r 5:19  # disp log for revs 5-19 in chronological order
    svn log -r 19:5  # disp log for revs 5-19 in rev. chronological order
    svn log -r 8     # disp log for rev 8 only
    svn log foo.c    # disp log for ``foo.c'' only
    svn log -v       # --verbose
    svn log ^/       # look in the top dir from a lower dir
    svn cat
    svn car -r <file>
    svn car -r <file> > cat.log
    svn annotate
    svn annotate <file>        # line-by-line attribution
    svn annotate <file>@BASE   # look at the unmodified form
    svn annotate <jpg/png/etc.> --force   # by default annotate skips binary files
    svn blame <file> -r <rev #>
    svn list
    svn list http://svn.example.com/repo/project     # look at versioned directories
    svn list -v http://svn.example.com/repo/project  # look in detail
    svn info     # show thw URLs of items involved in a conflict


### Add and Subtract

    svn add FOO
    svn delete FOO          # Immed. deletes the file & sched's the tree op.
    svn mkdir FOO           # Identical to `mkdir FOO; svn add FOO`.


### Re-order

    svn copy FOO BAR        # Immed. creates copy & sched's tree op. Opts: --parents
    svn move FOO BAR        # Same as `svn copy FOO BAR; svn delete FOO`

### Restore

    svn revert FOO          # Return to the latest repo. version. 
    svn reset

### Rename a branch

    svn move https://oldbranch https://newbranch

Then,

    svn switch https:://newbranch     # in existing repo checkouts


### Bundle w/o .svn dirs

    svn export http://svn.exmaple.com/svn/repo/trunk trunk-export        # export latest
    svn export http://svn.exmaple.com/svn/repo/trunk@1729 trunk-1729     # rev 1729
    svn export http://svn.exmaple.com/svn/repo/trunk -r 1729 trunk-1729  # rev 1729


### Misc. Admin

    svn cleanup # Get rid of old locks, etc.


### Revision Keywords in Action

    svn diff -r PREV:COMMITTED foo.c    # last change committed to foo.c
    svn log -r HEAD                     # log msg for latest repo commit
    svn diff -r HEAD                    # comp wrking copy to latest in repo
    svn diff -r BASE:HEAD foo.c         # unmod ver w/ latest ver in repo
    svn log -r BASE:HEAD                # commit logs for current dir since last update
    svn update -r PREV foo.c            # rewinds last change on foo.c, decr working rev
    svn diff -r BASE:14 foo.c           # comp unmod to rev 14


### Revision Dates in Action

    svn update -r {2006-02-17}
    svn update -r {15:30}
    svn update -r {15:30:00.200000}
    svn update -r {"2006-02-17 15:30"}
    svn update -r {"2006-02-17 15:30 +0230"}
    svn update -r {2006-02-17T15:30}
    svn update -r {2006-02-17T15:30Z}
    svn update -r {2006-02-17T15:30-04:00}
    svn update -r {20060217T1530}
    svn update -r {20060217T1530Z}
    svn update -r {20060217T1530-0500}
    svn log -r {2006-11-20}:{2006-11-29}


### Locks

    svn lock banana.jpg -m "Editing file for tomorrow's release."
    svn unlock banana.c           # Manually release a lock (auto release via commits.)
    svn info raisin.jpg | grep URL         # We need this URL for the next steps:
    svn unlock <url to>raisin.jpg          # Will fail unless we hold the token, but...
    svn unlock --force <url to>raisin.jpg  # This will break the lock.
    svn lock raisin.jpg                    # Will fail if already locked.
    svn lock --force raisin.jpg            # Steal the lock.
    svn update                             # Original locker can clear defunct locks.


### Properties

    svn commit -m "Fix the last bug." --with-revprop "test-results=all passing"
    svn log --with-all-revprops --xml <file>
    svn propset <name> 'text' <on file>
    svn propset copyright '(c) 2006 Red-Bean Software' calc/button.c
    svn propset license -F /path/to/LICENSE calc/button.c      # mulit-line in a file
    svn propedit copyright calc/button.c     # open an editor to change the property
    svn proplist <file>
    svn proplist -v <file>
    svn propget
    svn propdel <property> <file>            # delete a property
    svn propset svn:log "* button.c: Fix a warning." -r11 --revprop


### Ignoring File (through Properties)

    svn propset svn:ignore -F .cvsignore .   # turn on svn:ignore in dir .
    svn status --no-ignore                   # circumvent any ignores
    svn add --force .  # use instead of svn add * to have SVN respect ignores in bulk adds
    svn propedit svn:ignore .                 # brings up a buffer to entire file names


### Depth

* Set and operate under different ambient depths of the tree. Useful for checkout, 
  status, updates, etc. Encompases (obsoletes?) the recursive and non-recursive flags.
  Useful flags: `-set-depth`, `-set-depth exclude` (prune trees), `-set-depth infity`, 
  etc., `--depth empty`, `--depth immediates`, etc.


### Changelists

    svn changelist <name> files...
    svn changelist math-fixes integer.c mathops.c
    svn changelist math-fixes button.c
    svn changelist --remove button.c
    svn changelist ui-fix button.c       # Or skip the removal and direct assign.
    svn diff --changelist math-fixes     # Show only files in the changelist.
    svn commit --changelist ui-fix       # Only commit files from the list. (Clears the list)
    svn changelist math-bugs --changelist math-fixes --depth infinityy .  
    svn changelist --remove --changelist math-bugs --depth infinityy .  


### Branches

    svn copy http://svn.example.com/repos/calc/trunk \
             http://svn.example.com/repos/calc/branches/my-calc-branch \
             -m "Creating a private branch of /calc/trunk"    # Do svn copy on the server!
    svn checkout http://svn.example.com/repos/calc/branches/my-calc-branch
    svn merge ^/calc/trunk    # sync merge the trunk branch back into my branch
    svn merge ^/trunk/doc/INSTALL doc/INSTALL -c <rev #>  # Subtree merge
    svn mergeinfo ^/calc/trunk           # look at the mergeinfo
    svn revert . -R   # undo a merge that didn't go well...
    svn merge -c -303 ^/calc/trunk   # use a ``reverse-merge'' to undo a change 
    svn merge -c 335 ^/calc/trunk   # get just the changes in 335
    svn log -v -r <rev #> -g   # -g == --use-merge-history
    svn swtich ^/calc/branches/my-calc-branch


### Reintegrating a Branch

    svn merge ^/calc/trunk                 # Pull in main
    svn commit -m "final merge of trunk" 

Either checkout or `svn switch` to trunk

    svn merge --reintegrate ^/calc/branches/my-calc-branch
    svn commit -m "merged back into trunk"
    svn delete ^/calc/branches/my-calc-branch \
        -m "remove old merged branch"


### Recovering Deleted Items

    svn copy ^/calc/trunk/real.c@807 ./real.c     # save the history
    svn cat ^/calc/trunk/real.c@807 > ./real.c    # no history saved


### Tags

    # svn mkdir           # create the /calc/tags directory
    svn copy http://svn.example.com/repos/calc/trunk \
             http://svn.example.com/repos/calc/tags/release-1.0 \
             -m "Tagging the 1.0 release of the 'calc' project."
    
### Ignoring

    echo "*.o" > .svnignore
    svn propset svn:ignore -R -F .svnignore .  # read the file, apply recursively

Edit `$HOME/.subvsersion/config` to contain these lines:

    [miscellany]
    global-ignores = *.o *.lo *.la .*~ *~ .#* .DS_Store _ROOT*.cc _ROOT*.h

