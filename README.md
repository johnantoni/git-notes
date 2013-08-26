# GIT

## Installing GIT Hooks

    $ cd .git
    $ rm -fr hooks
    $ git clone git://github.com/zoocasa/git-hooks.git hooks 

## Common Development Tasks

### Pruning Branches

    git fetch --prune
    git prune
    git gc --aggressive

### Fetching Remote Branches

    git fetch --all

### Create a new Branch based on the current commit

    git co -b [new-branch-name]

### Track Branch (git 1.8)

    git branch -u origin/new-feature

### Amend a Commit

    git commit -m 'initial commit'
    git add forgotten_file
    git commit --amend

### Ammend a Commit (rewriting remote branch's history)

    git co HEAD~1
    git commit -m 'forgotten file'
    git push origin branch-name --force

### Get all Changes from Parent branch

Say you're on new-feature and you want to pull the changes from master

##### First make sure your local master is up-to-date

    git co master
    git pull --rebase -p

-p means prune any obsolete branches

##### Now checkout your new-feature branch and pull the changes from master

    git co new-feature
    git rebase master

When you rebase it will stop if there's merge conflicts introduced from master.

If you get any, fix them with your text editor then:

##### Check what's been changed:

    git status
    git diff

Add your resolutions:

    git add .

Continue rebasing:

    git rebase --continue

If nothing was changed with resolution:

    git rebase --skip

Once resolved & rebased you will now be back on the new-feature branch with an updated commit history.

To push your changes to the branch you'll need to force-push as the history in the remote branch will be out of date.

    git push -f origin new-feature

## Cherry Pick one commit into current branch

Find the commit id for the one you want to apply to the top of your current branch, then:

    git cherry-pick [commit hash]

More [here](http://ariejan.net/2010/06/10/cherry-picking-specific-commits-from-another-branch/)

## Rollback Local to be same as Remote

    git fetch origin
    git reset --hard origin/master

## Commands

### git r
show current branch history

### git ra
show all history

### git push --set-upstream origin <branch-name>
*--set-upstream* sets what ref we'll be pushing to so we don't have to specify every time.
This won't have any effect as we've used [default=nothing] in our .gitconfig so we'll have to specify the ref on each push.

### git pull --rebase
Doing 'git pull' is fine but if you're working on a branch others are actively using this will add a merge message to the log messing up the log history. Using --rebase will do a pull then rebase and keep the log clean.

### git stash
Stash your un-committed changes

### git stash pop
Restore your stashed changes

### git stash list
List all stashed changes

### git stash pop[1]
Restore stashed change at location 1

### git merge --ff-only
Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a fast-forward.

### git branch -d <branch-name>
Delete local branch

### git push origin --delete <branch-name>
Delete remote branch

### git ri <branch-name>
Start interactive rebase

### git rebase --abort
Abort rebase

### git reset --soft
Does not touch the index file nor the working tree at all (but resets the head to <commit>, just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.

### git reset --hard
Resets the index and working tree. Any changes to tracked files in the working tree since <commit> are discarded.

### git reset --hard HEAD~3
Rewind branch 3 commits back, destroying those commits

### git grep [search term]
Search committed code in a git repo http://stackoverflow.com/questions/2928584/how-to-grep-search-committed-code-in-the-git-history

### git blame [file]
See commit history for file.

### git branch -a
See both local and remote branches

### git branch -l
See local branches

### git branch -r

See remote branches

## Tools

* TIG[https://github.com/jonas/tig]

## Notes

### Rebase Types

    p, pick = use commit
    r, reword = use commit, but edit the commit message
    e, edit = use commit, but stop for amending
    s, squash = use commit, but meld into previous commit
    f, fixup = like "squash", but discard this commit's log message
    x, exec = run command (the rest of the line) using shell

## Links

* [revert to previous commit](http://stackoverflow.com/questions/4114095/git-revert-to-previous-commit-how)
* [25 Tips for Intermediate Git Users](http://andyjeffries.co.uk/articles/25-tips-for-intermediate-git-users)
* [GitX for OSX](https://github.com/rowanj/gitx)

