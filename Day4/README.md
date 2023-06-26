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

## Lab - Merging changes that involve merge conflicts
```
git branch main
touch file2.txt
echo "Line 1" > file2.txt
git commit -m "Added file2.txt in main branch"

echo "Hotfix123" >> file1.txt
git commit -am "Hotfix123 done in main branch"


git checkout dev-1.0
echo "ENH12345" > file1.txt
git commit -am "Implemented ENH12345 in dev-1.0 branch"
git log --oneline

git checkout main
git merge dev-1.0
```

Now edit the file1.txt and resolve the conflicts manually accepting changes from both main and dev-1.0 branch. Once the manually the merge conflicts are resolved, you need to commit the changes
```
git commit -am "Resolved merge conflicts in main branch"
git log --oneline
cat file1.txt
cat file2.txt
```

## Lab - Git rebase ( an alternate for git merge )
```
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ touch file1.txt
jegan@tektutor.org:~/git-demo$ git init
Initialized empty Git repository in /home/jegan/git-demo/.git/
jegan@tektutor.org:~/git-demo$ echo "M1" > file1.txt 
jegan@tektutor.org:~/git-demo$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file1.txt

nothing added to commit but untracked files present (use "git add" to track)
jegan@tektutor.org:~/git-demo$ git add file1.txt 
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
jegan@tektutor.org:~/git-demo$ git commit -m "Added M1"
[main (root-commit) a9c5a12] Added M1
 1 file changed, 1 insertion(+)
 create mode 100644 file1.txt
jegan@tektutor.org:~/git-demo$ git status
On branch main
nothing to commit, working tree clean
jegan@tektutor.org:~/git-demo$ git log --oneline
a9c5a12 (HEAD -> main) Added M1
jegan@tektutor.org:~/git-demo$ echo "M2" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added M2"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main 534dea8] Added M2
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ echo "M3" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added M3"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main a779cfb] Added M3
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ git log --oneline
a779cfb (HEAD -> main) Added M3
534dea8 Added M2
a9c5a12 Added M1
jegan@tektutor.org:~/git-demo$ git checkout -b dev-1.0
Switched to a new branch 'dev-1.0'
jegan@tektutor.org:~/git-demo$ echo "D1" > file1.txt 
jegan@tektutor.org:~/git-demo$ ls
file1.txt
jegan@tektutor.org:~/git-demo$ git status
On branch dev-1.0
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
jegan@tektutor.org:~/git-demo$ git restore file1.txt
jegan@tektutor.org:~/git-demo$ ls
file1.txt
jegan@tektutor.org:~/git-demo$ cat file1.txt 
M1
M2
M3
    
jegan@tektutor.org:~/git-demo$ echo "D1" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added D1 in dev-1.0 branch"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[dev-1.0 5880a26] Added D1 in dev-1.0 branch
 1 file changed, 1 insertion(+)
    
jegan@tektutor.org:~/git-demo$ echo "D2" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added D2 in dev-1.0 branch"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[dev-1.0 4b3af65] Added D2 in dev-1.0 branch
 1 file changed, 1 insertion(+)
    
jegan@tektutor.org:~/git-demo$ git status
On branch dev-1.0
nothing to commit, working tree clean
    
jegan@tektutor.org:~/git-demo$ git log --oneline
4b3af65 (HEAD -> dev-1.0) Added D2 in dev-1.0 branch
5880a26 Added D1 in dev-1.0 branch
a779cfb (main) Added M3
534dea8 Added M2
a9c5a12 Added M1
    
jegan@tektutor.org:~/git-demo$ git checkout main
Switched to branch 'main'
jegan@tektutor.org:~/git-demo$ git log --oneline
a779cfb (HEAD -> main) Added M3
534dea8 Added M2
a9c5a12 Added M1
    
jegan@tektutor.org:~/git-demo$ git rebase dev-1.0
Successfully rebased and updated refs/heads/main.
    
jegan@tektutor.org:~/git-demo$ git log --oneline
4b3af65 (HEAD -> main, dev-1.0) Added D2 in dev-1.0 branch
5880a26 Added D1 in dev-1.0 branch
a779cfb Added M3
534dea8 Added M2
a9c5a12 Added M1
</pre>


