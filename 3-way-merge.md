#### anatomy of a 3-way merge

##### git merge

    [-----local-----] [-----base-----] [-----remote-----]
    
* Base contains original without remote/local conflicting changes and only non-conflicting changes.
* Local are the conflicting changes from your local machine
* Remote are the changes coming from the remote (e.g. github repository)

##### git rebase

This changes if your rebasing as local changes will be applied on top of any remote changes, so:

    [-----local-----] [-----base-----] [-----remote-----]

When you do a git pull --rebase your are updating the commit history with changes from the remote, then applying your local changes on top of those commits.

* Local will contain the conflicting changes from all the commits leading up to the merge, so will also include changes from the remote.
* Base will contain the original and any non-conflicting changes.
* Remote will contain the changes you have done locally that conflict with the repositories combined commits.

##### Links

* [What's the difference between 'git merge' and 'git rebase'?](http://stackoverflow.com/questions/16666089/whats-the-difference-between-git-merge-and-git-rebase)
* [learn git branching](http://pcottle.github.io/learnGitBranching/)
