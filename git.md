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

    git -d branchname

remote:
    
    git push origin :branchname

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
