# Git Overview
Version Control system
## Commands
```
//Initialisation
git init 
ls -a (show hidden .git file

//Commiting
git status
git add medals.html
git commit -m "Add medals.html" (meassages should answer"This commit will?")
git config --globsl user.email "ks.kennysoh@gmail.com"
git config --globsl user.name "Kenny Soh"

//Viewing Changes
git diff (shows what changed with prevoius stagging area or commit)
 git diff --staged (staged vs commit)
 
//Removing a file
rm tin.html
git rm tin.html
git commit -m "removed tin.html"

git mv silver.txt silver.html //Moving Files

//Unstaging changes
git status //Shows reset instruction
git reset HEAD medals.html //Unstage staged medals.html

//Discarding File Modifications & Undo File deltion back to Commit. 
git status
git checkout -- medals.html //discard changes

//Showing all Commit SHAs and Undoing Commits
git log
git revert c02bf //(first 5 letters, revert back to c02bf)

git revert HEAD // HEAD is the latest commit ,( revert revert c02bf)

//Cloning repo
git clone https://github.com/treehouse-courses/novel.git novel //clones to local novel directory.
cd novel

//Pulling Changes
git remote //ensure remote repo is setup , returns "Origin"
git pull

//Adding Remotes
git remote add myclone ../myclone
git branch
git pull myclone master

//Pushing 
git push -u origin masters //-u send upstream, sends this repo and branch in the future

```
