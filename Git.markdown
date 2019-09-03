# References

* git: http://git-scm.com/about
* git: http://git-scm.com/book
* git: http://www.github.com
* git-flow: http://nvie.com/posts/a-successful-git-branching-model/

## Get Help

```
git help            # Also, "git --help {}".
git help {command}
```

## Get the (C) Source Code

```
git clone git://github.com/gitster/git.git
```

## `.gitignore`

1. Blank lines are ignored, and a pound sign (`#`) can be used for comments.
2. A simple, literal filename matches a file in any directory with that name.
3. A directory name is marked by a trailing slash character, like so/
4. A pattern containing shell glob characters (`*`) is expanded as a shell
glob pattern, e.g. `debug/32bit/*.o`
5. An initial ! inverts the pattern over the line.
6. You may have a gitignore in any directoy in the repository, and files in
lower directories override higher directories.

## Configure Git

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global core.editor vim  
```

## Check Your Configuration

```
git config -l
```

## Create an Alias (Example)

```
git config --global alias.show-graph 'log --graph --abbrev-commit --pretty=oneline'
git show-graph
```

## Work in Living Color

```
git config --global color.diff true
git config --global color.status true
git config --global color.branch true
git config --global color.interactive true
```

## Start a Repository

Perform in the directory you wish to be the root: `git init`

## Add (Stage) to a Repository

```
git add {files}   # e.g., "git add ." after "git init". Must commit.
git add {files}   # Also to "re-add" after clearing conflicts in a merge!
                  # tracked: "git add {file}; git commit" == "git commit -a"
git add -u        # Add to the index all the changes of files already tracked.
```

## Remove from a Repository

```
git rm {file}            # Also removes the file. Must commit.
git rm --cached {files}  # Staged only.
```

## Commit to a Repository

```
git commit --dry-run       # Don't actually perform the commit.
git commit -a              # Commit all, also "--all"
git commit {file}
git commit -m "Message" {file}
git commit --ammend         # Change the top commit
git cherry-pick {commit}    # Bring a single commit from another branch.
git revert {commit}         # "Remove" a given commit from earlier.
```

## Restore a Commit

```
git checkout {SHA1 hash}       # You only need enough of the hash...
git checkout {tag}             # Restore to a {tag}.
git checkout master            # The master "tag" refers to the last commit.
```

## Recover a File

```
git checkout {file}
git checkout {SHA1 hash} {file}           # Get back a specific version.
git ls-files -d | xargs git checkout --   # Get all accidentally removed files.
```

## Clone a Remote Repository

```
git clone git://github.com/gnperdue/GitTutorial.git
git clone git://github.com/tpope/vim-commentary.git     # If you like vi...
```

## Push to a Remote Repository

```
git remote add origin https://github.com/gnperdue/GitTutorial.git
git push -u origin master
```

## Examine a Remote Repository

```
git remote                        # Show a list of existing remote
git remote -v                     # Also, --verbose
git remote show origin
git remote rm {reference}         # Drop a remote.
git remote rename {old branch} {new branch}
```

## Fetch Data from a Remote Repository

```
git fetch {repository}            # Find the repository name with "git remote".
                                  # This just gets the data. It does not merge!
                                  # Follow with "git merge" - e.g. "git fetch
                                  # origin" followed by "git merge origin"
git fetch --dry-run               # Don't perform a fetch, just  show what
                                  # *would* have happened.
```

## Pull Data from a Remote Repository

```
git pull {repository}             # Fetch *and* merge.
```

## Check out a pull request

Here, `ID` is the pull request number.

```
git fetch upstream pull/ID/head && git checkout FETCH_HEAD && \
  git checkout -b test_ID
```

This gets the pull, checks us out into a 'Detached HEAD', and then puts us onto
a test branch.

## Force pull to overwrite local changes

```
git fetch --all && git reset --hard origin/master
```

## Create a Tree Object from the Current Index

```
git write-tree  
```

## Examine a Repository

```
git show                          # Examine various objects.
gitk                              # Graphical representation of the repository.
git status                        # What is staged and not, what branch are you
                                  # on, how far ahead is the local, etc.
git log                           # Show the *reachable* commits.
git log --graph --abbrev-commit --pretty=oneline
git ls-files -s
git ls-files --stage
git log -S{string}                # "Pickaxe" - search file diff history.
git log --merge --left-right -p
git reflog                        # Look at the commit history...
```

## Examine a Commit

```
git show {sha1}                   # May use the first N significant characters
git show --pretty=fuller
git rev-parse {sha1}
```

## Edit History

```
git commit --amend -m "New message"   # ONLY if you haven't pushed yet
                                      # old message will still show in `reflog`
                                      # but not in `log`
```

## Refer to Commits Relatively

Relative Commit Names
^ the penultimate commit (e.g., master^, master^^, etc.)
~ the previous commit in the ancestry chain.

```
git log --pretty=short --abbrev-commit master~4..master~2   
                                    # Since..Until - used for commit ranges.
```

## Examine a Symbolic Ref

```
git symbolic-ref HEAD
```

## Look at the Content of a File

```
git cat-file -p {sha1}
```

## Create a Tag

```
git tag                                   # List available tags.
git tag -l 'v1.2.*'                       # List only the tags beginning with
                                          # v1.2.{wildcard}.
git tag -a {tag name}                     # Make an annotated tag.
git tag -s {tag name}                     # Make a signed tag (with GPG
                                          # credentials).
git tag -m "Message" {tag name} {files}
git push origin {tag}                     # Apply a tag to the remote server.
git tag -d {tag name}                     # Delete a tag.
git push origin :{tag name}               # Apply deleted tag to the remote.
git show {tag name}
git checkout {tag name}                   # Check out a tag; end up left in a
                                          # detached HEAD
git checkout -b {branch name} {tag name}  # Check out a tag w/o being left in
                                          # detached HEAD

git tag -a {tag name} {hash} -f           # update a tag to be forced to point
                                          # at a new hash
git push origin --tags -f                 # force the new tag onto the server
```

Example workflow for creating and pushing a tag:

```
git tag -a R-2_9_0.1 -m "lamp tag for GENIE R-2_9_0 with corrected SVN paths on HepForge"
git push origin --tags
```

Example workflow for moving a tag:

```
git tag -a R-2_9_0.1 80000766b216b23c0 -f  # point to new commit
git push origin --tags -f
git show <tag-name>         # look at a tag (can `show` other stuff too)
```

Look at remote tags

```
git ls-remote --tags
```

`git ls-remote` is generally useful. A nice little workflow

```
git remote -v
git fetch origin
git checkout tags/boffo -b boffo_working
```

Delete a tag when it has the same name as a branch

```
git push --delete origin refs/tags/R-2_10_2
```

## Assign Blame

```
git blame {file}
git blame -L {first line},{last line} {file}      # Blame over a range.
```

## Listing the Branches in the Repository

```
git branch                                # Topic branches
git branch -r                             # Remote branches
git branch -a                             # Topic and remote branches
```

More on remote branches

```
git remote show origin
git checkout --track upstream/<branch name>  # track remote branch
```

## Examine a Branch

```
git show-branch                   # Shows head?
git show-branch --more=N          # Goes N deep.
git show-branch -r                # See remote in detail!
```

## Find a Branch Starting Point

```
git merge-base {original branch} {dev branch}
```

## Create a Branch

```
git branch {name*} {starting commit - default HEAD}   # Does not switch to the
                                                      # branch! (*wildcard ok)
get checkout {name}                    # Switch to the branch.
git checkout -b {name}                 # Create a branch *and* switch to it.
                                       # This is short-hand for `git branch {x};
                                       # git checkout {name}`
git fetch; git checkout {remote name}  # Checkout a remote branch
```

## Switch into a Branch

```
git checkout {branch}                 # git checkout -b {branch} for new one
git checkout --track origin/{branch}  # follow an existing remote
```

## Merging into a Branch

A useful stackoverflow post on reverting to previous commits is:

    http://stackoverflow.com/questions/4114095/revert-to-a-previous-git-commit

Commands:

```
git checkout -m {branch}          # Bring uncommitted changes with you. Watch
                                  # for merge conflict indicators!
git merge {branch}                # Remember, you need to be on the branch you
                                  # want changes merged into.
git reset --hard HEAD             # Abort a merge and go back to the state right
                                  # before we typed "merge". Careful with dirty
                                  # repos.
git reset --hard ORIG_HEAD        # Abort a merge and go back to right before we
                                  # typed merge after the merge is complete.
git merge -s {strategy} {branch}  # Careful!
```

## Deleting a Branch

```
git branch -d {branch}            # You cannot delete the current branch. You
                                  # can override safety checks with "-D".
git push origin --delete {branch} # Delete the remote branch.
```

## Tracking a Remote Branch

```
git merge origin/remote_branch_name   # merge a remote branch into current
git checkout --track origin/{branch}
git checkout -b {new name} origin/{branch}
```

## Sync to a remote branch on GitHub

Example workflow (`$BRANCH` could be `master` or some other branch):

```
git remote -v
git remote add upstream git@github.com:${USER}/${REPONAME}.git
git remote add upstream https://github.com/${USER}/${REPONAME}.git  # alt
git fetch upstream
git merge upstream/${BRANCH}
```

And, if you screw up the origin

```
git remote rm upstream              # or `destination`, etc.
```

## Check out a file from another branch

```
git checkout other_branch the_file   # Bring `the_file` from `other_branch`
                                     # in.
```

## Cleanup Unnecessary Files

```
git gc                              # Often will compress snapshots into diffs
                                    # (happens periodically automatically).
```

## Taking Diff's

```
git diff                            # Difference between the working directory
                                    # and the index.
git diff {commit}                   # Difference between the working directory
                                    # and the given commit.
git diff --cached {commit}          # Difference between staged changes and a
                                    # given commit.
git diff {commit1} {commit2}        # Difference between two commits.
git diff --M                        # Detects renames and generates a
                                    # simplified output.
git diff -w {or --ignore-all-space} # Do not consider whitespace changes to be
                                    # significant.
git diff --stat                     # Add statistics.
git diff --color                    # Colorize the output.
```

## Diff's between branches

```
git diff integration_b master -- src/Algorithm/Makefile
git diff integration_b master -- src/Algorithm/Makefile src/BaryonResonance/Makefile
git diff integration_b master -- `find . -name "Mak*"`
git diff --shortstst integration_b master      # just the total number of
                                               # changes
```

## Change to a Specific State

```
git reset HEAD                 # Unstage changes, restore.
git reset HEAD^                # Unstage changes, restore to commit just   
                               # before HEAD. (Remove the topmost commit, often
                               # explicity "--mixed".)
git reset --soft {commit}      # Go back to {commit}, but leave index and
                               # working directory contents unchanged.
git reset --soft HEAD^         # Get another shot at the commit message only
                               # ("git commit --amend" is better).
git reset --mixed {commit}     # Point HEAD to {commit}, modify index contents,
                               # but leave working directory unchanged.
                               # Mixed is default!
git reset --hard {commit}      # Point HEAD to {commit}, modify index contents
                               # and working directory.
```

## Squash the last N commits

1. ~> `git reset --soft HEAD~N`             # `N` is a number (e.g. 2)
2. ~> `git commit -m "new commit message"`  # changes will already be staged

*Note:* if pushing squashed commits will change the history on the remote, you
_must_ put a `+` in front of the branch name, e.g.

```
git push origin +name-of-branch
```

## Squash many commits from a feature branch (significant rewrite of history)

1. ~> `git checkout master && git pull`
2. ~> `git merge feature_branch`         # local work
3. ~> `git reset origin/master`          # back to origin state

Now, all changes are considered as unstaged changed and we can stage and commit
them into one or more commits.

## Another take on squashing commits

H/T https://github.com/wprig/wprig/wiki/How-to-squash-commits
1. Make sure your branch is up to date with the master branch (work on the
feature branch here).
2. Run `git rebase -i master`.
3. You should see a list of commits, each commit starting with the word "pick".
Make sure the first commit says "pick" and change the rest from "pick" to
"squash". This will squash each commit into the previous commit, which will
continue until every commit is squashed into the first commit.
4. Save and close the editor. It will give you the opportunity to change the
commit message.
5. Save and close the editor again.
6. Then you have to force push the final, squashed commit:
    `git push origin branch -f`.


## Alter Where a Series of Commits is Based

```
git rebase {branch}      # DON'T rebase commits you've pushed to a public repo!
git rebase -i master~3   # Interacive rebase (whoah!) going back 3 commits.
```

## Stash Work

Put everything into a quick stash and get a clean working area. ("Interrupted
Work")

```
git stash save "message"            
```

Restore (& drop) a stashed state. Git will attempt a merge. (Only pop into a
"clean" area!)

```
git stash pop                       
```

"Look" at the stash.

```
git show-branch stash               
```

Restore the stash but don't drop it from the index.

```
git stash apply                     
```

Drop the stash (so, "pop = apply (followed by) drop").

```
git stash drop                      
```

Convert the stash into a new branch based on the commit at the time the stash
was stashed.

```
git stash branch                    
```

List the stashes (that haven't been dropped), `stash@{1}` is older than
`stash@{0}`.

```
git stash show                      
```

Other:

```
git stash save "message" --include-untracked
git stash save "message" --all      
```

## Move uncommitted work to a new branch (from `master`)

```
git checkout -b new_branch
git add files
git commit
```

At this point, `master` has been reset:

```
git checkout master  
```

`new_branch` will contain the changes

```
git checkout new_branch   
git push origin new_branch
```

## Just take the remote state, dangit!

Two steps:

1. `git fetch`
2. `git reset --hard origin/master`   

Where, of course, `master` is the branch you want.

## Merge branches from GitHub pull requests by hand to a new branch

GitHub puts these instructions on the pull request if you look for them, but
here they are anyway (mostly as a one-time log of everything working):

0. ` git clone git@github.com:GENIEMC/GENIE_2_9_0.git`
1. `cd GENIE_2_9_0`
2. `git checkout -b igor144-rein_sehgal master`
3. `git pull https://github.com/igor144/GENIE_2_9_0.git rein_sehgal`
4. `git push origin igor144-rein_sehgal`

GitHub goes on to tell you how to merge into master instead of pushing the new
branch, but I want to push the new branch...
