---
layout: bento
title: dr blinken | git
---


GIT
===


_work in progress_

##stage files for commit: 

    git add <file>
##unstage files:
    git rm --cached <file> 

see [Git Book](http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository)


remove files that have been removed without git

    git rm $(git ls-files --deleted)


Info
-----

    git log

see changes in a single commit:

    git show <commit>

Undoing
-------
### delete last commit: see [stackoverflow](http://stackoverflow.com/questions/927358/undo-last-git-commit)

Committing 
----------

To stage deleted files for commit: 
    git add . -A 

### rebase

[Rebase man page](http://git-scm.com/docs/git-rebase)
[Rebase chapter in git book](http://git-scm.com/book/de/Git-Branching-Rebasing)


    git rebase -i <hash of first commit you don't wanna change>

two default editors open: one to change the commits, and if you're squashing
commits together, one to edit a joined commit message

It's best to do this before merging a branch / pushing upstream.
If you already pushed upstream - to github e.g. - you can push the changes with
     git push origin master -f

which should absolutely only be done if noone has work based on that upstream rep.

Git Links
---------

* [Git Book](http://git-scm.com/book/)