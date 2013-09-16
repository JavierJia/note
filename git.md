# show the changed file between different branches:

    git diff --name-status master..branchname

# push branch
    
    git push origin branchname

# change remote 
    git remote -v
    git remote rm origin
    git remote -v
    git remote add origin https://xxxx.git

# delete branch
local:

    git branch -d branchname

remote:
    
    git push origin :branchname

remove obsolete branc
```
git remote prune origin
```

# add upstream:

    git remote add upstream https://xxxx.git

# 'revert' idea 
just checkout :
    git checkout -b old-state 0d1d7fc32

If, on the other hand, you want to really get rid of everything you've done since then, there are two possibilities. One, if you haven't published any of these commits, simply reset:

    # This will destroy any local modifications
    # Don't do it if you have uncommitted work you want to keep
    git reset --hard 0d1d7fc32

# push to server

    git push -u origin marys-feature

This command pushes marys-feature to the central repository (origin), and the -u flag adds it as a remote tracking branch. After setting up the tracking branch, Mary can call git push without any parameters to push her feature.

# branch change name

    git branch -m <oldname> <newname>

# git merge confilict
http://stackoverflow.com/questions/161813/how-do-i-fix-merge-conflicts-in-git

    git mergetool
    git diff
    git checkout --ours ourfiles
    git checkout --theirs theirfiles
    git add ourfiles theirfiles
    git commit -m "resolve conflicts"

## merging using vimdiff tool
http://vimcasts.org/episodes/fugitive-vim-resolving-merge-conflicts-with-vimdiff/

    :diffget //2 – fetches the hunk from the target parent (on the left)
    :diffget //3 – fetches the hunk from the merge parent (on the right)

final check

    git pull origin master

# git fetch remote branch
```
git fetch origin
git checkout -b test origin/test
```
# git diff
'''bash
    # diff between commits 14b8... and b410...
    git diff 14b8..b410
    # only include diff of specified files
    git diff 14b8..b410 path/to/file/a path/to/file/b
'''

# git with patch
'''bash
git diff > patchfile
patch -p1 < patchfile
'''

# git squash

The rebase -i idea is suggested in this link. 

Basically, "Rebasing is the process of moving a branch to a new base commit". And git rebase --interactive (or -i) mode give us a chance to edit the commits. 
The detail process is introduced in the blog: http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html

Here is the quick command if you don't want to go through those blogs. Suppose you are working on one branch, and have 4 commits logs:

run 
```
git log --pretty=oneline
```
You will get these commits details:
```
01d1124 Adding license
6340aaa Moving license into its own file
ebfd367 Jekyll has become self-aware.
30e0ccb Changed the tagline in the binary, too.
7c53e0d I've already pushed.
```
We want to squash the latest four commit as one, then we rebase the current branch from his own certain version.
```
git rebase -i HEAD~4
#or
git rebase -i 7c53e0d
```
Then it will show you something like this:
```
$ git rebase -i HEAD~4 
pick 01d1124 Adding license 
pick 6340aaa Moving license into its own file 
pick ebfd367 Jekyll has become self-aware. 
pick 30e0ccb Changed the tagline in the binary, too. 
 
# Rebase 60709da..30e0ccb onto 60709da 
# 
# Commands: 
# p, pick = use commit 
# e, edit = use commit, but stop for amending 
# s, squash = use commit, but meld into previous commit 
# 
# If you remove a line here THAT COMMIT WILL BE LOST. 
# However, if you remove everything, the rebase will be aborted. 
#
```
Change it into below:
```
$ git rebase -i HEAD~4 
pick 01d1124 Adding license 
s 6340aaa Moving license into its own file 
s ebfd367 Jekyll has become self-aware. 
s 30e0ccb Changed the tagline in the binary, too. 
  
# Rebase 60709da..30e0ccb onto 60709da 
# 
# Commands: 
# p, pick = use commit 
# e, edit = use commit, but stop for amending 
# s, squash = use commit, but meld into previous commit 
# 
# If you remove a line here THAT COMMIT WILL BE LOST. 
# However, if you remove everything, the rebase will be aborted. 
#
```  
And then exit your editor ( it will show another window to let you change the details of commit message), then everything is done. All the squashed commit is disappeared. Then we can continue work on it or push it to origin.

There is one small problem with this approach which is the conflict. It's common that we change the same line back and force. In that case the rebase will show you the following message:
```
  error: could not apply e007062... Add licencse

  When you have resolved this problem run "git rebase --continue".
  If you would prefer to skip this patch, instead run "git rebase --skip".
  To check out the original branch and stop rebasing run "git rebase --abort".
  Could not apply e007062... conflict now
```
Don't worry, if we are sure that we just want the final changes, we don't need to merge these conflicts. We can checkout the remote version totally by:
```
  git checkout --theirs /conflict/file/name /name2
# or we directly checkout the whole path:
  git checkout --theirs .
```
  Then tell the git that conflict is resolved and continue rebasing by :
```
  git add /conflict/files 
  git rebase --continue
```
  Rebase work through each commit one by one, thus we may have another conflict later. Continue do the above commands until successfully rebased. 
