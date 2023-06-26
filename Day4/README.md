# Day 4

## Git merge - Fast Forward 

Create a new local repo
```
cd ~/git-demo
rm -rf .git
rm *

git config --global init.defaultbranch main
git init
touch file1.txt
git add file1.txt
git commit -m "Initial commit."


echo "Line 1" >> file1.txt
git commit -am "Implemented ENH12345 in main branch"

echo "Line 2" >> file1.txt
git commit -am "Implemented ENH12346 in main branch"

echo "Line 3" >> file1.txt
git commit -am "Implemented ENH23461 in main branch"

git log --oneline
```

Let's create the dev-1.0 branch
```
git checkout -b dev-1.0
git log --oneline
```

Listing the branches. The branch that precedes with "*" and shown in green color is the currently active branch
```
git status
git branch
```

Let's make some changes in the dev-1.0 branch
```
git checkout dev-1.0  # Switching to dev-1.0 branch

echo "Bug123254" >> file1.txt
git commit -am "Fixed bug BUG123245 in dev-1.0 branch"

echo "ENH325444" >> file1.txt
git commit -am "Implemented ENH325444 in dev-1.0 branch"

git log --oneline
```

Now switch back to main branch and see the changes done in dev-1.0 branch is not there
```
git log --oneline
ls
cat file.txt
```

Now let's merge the dev-1.0 changes into the main branch. We need to ensure first we are in the main branch
```
git checkout main
git merge dev-1.0
git log --oneline
cat file1.txt

```



