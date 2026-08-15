# Setup
git config --global user.name "Soham"
git config --global user.email "email@gmail.com"

# Basic flow
git init                    # start repo
git status                  # check changes
git add .                   # stage all files
git add filename            # stage one file
git commit -m "message"     # save snapshot
git push                    # upload to GitHub
git pull                    # download from GitHub

# Branches
git branch                  # list branches
git checkout -b newbranch   # create + switch
git checkout main           # switch to main
git merge branchname        # merge branch

# Remote
git remote add origin URL   # connect to GitHub
git clone URL               # download repo

# Useful
git log                     # commit history
git diff                    # see changes
git stash                   # save temp changes
git reset --hard HEAD       # undo all changes
