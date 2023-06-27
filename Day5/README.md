# Day 5

## What is pull request in GitHub?
- Pull request is a way a developer will be able to notify other team members that he/she has implemented the enhancement or ready with a fix for a bug reported. It is through pull request a developer would be request other developers for reviewing the code.

## Lab - Creating a pull-request
```
cd ~/git-demo
rm -rf .git
rm *

git init
touch file1.txt
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/tektutor/github-demo-june2023-china.git #You need to replace this with your gd training github repo url

git remote -v

echo "Line 1" > file1.txt
git commit -am "Implemented Enhancement ENH12345"

echo "Line 2" > file1.txt
git commit -am "Implemented Enhancement ENH54345"

git checkout -b feature12345
echo "Feature12345" > file1.txt
git commit -am "Implemented Enhancement Feature12345"
git log --oneline
cat file1.txt
git status
```

Now assume you are done with the Feature12345, let's request other team members for code review to merge the changes into the main branch.
```
git push -u origin feature12345 main
```
You will get an output as shown below 
<pre>
jegan@tektutor.org:~/git-demo$ git push -u origin ENH734234  main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 287 bytes | 287.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'ENH734234' on GitHub by visiting:
remote:      https://github.com/tektutor/github-demo-june2023-china/pull/new/ENH734234
remote: 
To https://github.com/tektutor/github-demo-june2023-china.git
 * [new branch]      ENH734234 -> ENH734234
Branch 'main' set up to track remote branch 'main' from 'origin'.
Branch 'ENH734234' set up to track remote branch 'ENH734234' from 'origin'.  
</pre>

Now open the URL below to create the pull-request in the GitHub repo
<pre>
https://github.com/tektutor/github-demo-june2023-china/pull/new/ENH734234
</pre>

Now other team members can go the gd training GitHub repo and try to approve the pull-request. Post the approval, you will be able to merge your feature branch changes to the main branch.


## What is a git patch?
- In earlier version of GitHub, the pull-request feature was not supported
- Hence, the only way someone can share their code changes for code-review to other team members was by using git patch
- Apart from code review, git patch also helps people email their code changes to fellow senior team members in case they don't have code commit access permission
- is a text file, hence sharing via email is pretty easy
- even today, some opensource projects still use git patch for code reviews

## Lab - Creating a patch and apply the patch onto some branch
<pre>
jegan@tektutor.org:~/git-demo$ git diff c7056c9 9a85f23 > hotfix123.patch
  
jegan@tektutor.org:~/git-demo$ cat hotfix123.patch 
diff --git a/file1.txt b/file1.txt
index 6ad36e5..21a27d8 100644
--- a/file1.txt
+++ b/file1.txt
@@ -1,3 +1,4 @@
 Line 1
 Line 2
 Line 3
+Hotfix123
  
jegan@tektutor.org:~/git-demo$ git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
  
jegan@tektutor.org:~/git-demo$ git checkout -b fix123
Switched to a new branch 'fix123'
  
jegan@tektutor.org:~/git-demo$ cat file1.txt 
Line 1
Line 2
Line 3
  
jegan@tektutor.org:~/git-demo$ cat hotfix123.patch 
diff --git a/file1.txt b/file1.txt
index 6ad36e5..21a27d8 100644
--- a/file1.txt
+++ b/file1.txt
@@ -1,3 +1,4 @@
 Line 1
 Line 2
 Line 3
+Hotfix123
  
jegan@tektutor.org:~/git-demo$ git apply -v hotfix123.patch
Checking patch file1.txt...
Applied patch file1.txt cleanly.
  
jegan@tektutor.org:~/git-demo$ vim hotfix123.patch 
jegan@tektutor.org:~/git-demo$ cat file1.txt 
Line 1
Line 2
Line 3
Hotfix123  

jegan@tektutor.org:~/git-demo$ git status
On branch fix123
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	hotfix123.patch

no changes added to commit (use "git add" and/or "git commit -a")
    
jegan@tektutor.org:~/git-demo$ cat file1.txt 
Line 1
Line 2
Line 3
Hotfix123
    
jegan@tektutor.org:~/git-demo$ git add file1.txt 
    
jegan@tektutor.org:~/git-demo$ git commit -m "Applied fix123 patch on the fix123 branch"
[fix123 f419c57] Applied fix123 patch on the fix123 branch
 1 file changed, 1 insertion(+)
    
jegan@tektutor.org:~/git-demo$ git log --oneline
f419c57 (HEAD -> fix123) Applied fix123 patch on the fix123 branch
c7056c9 (origin/main, main) Implemented ENH43453453
dce4cda Implemented ENH4234234
bad80b4 Implemented ENHC12345
d16c18b Initial commit.  
</pre>

## Lab - Using cherry pick
<pre>
jegan@tektutor.org:~/git-demo$ git init
Initialized empty Git repository in /home/jegan/git-demo/.git/
jegan@tektutor.org:~/git-demo$ ls -lha
total 12K
drwxrwxr-x  3 jegan jegan 4.0K Jun 27 12:59 .
drwxr-x--- 43 jegan jegan 4.0K Jun 27 12:37 ..
drwxrwxr-x  7 jegan jegan 4.0K Jun 27 12:59 .git
	
jegan@tektutor.org:~/git-demo$ touch file1.txt
jegan@tektutor.org:~/git-demo$ git add .
jegan@tektutor.org:~/git-demo$ git commit -m "Initial commit."
[main (root-commit) 38f4992] Initial commit.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1.txt
	
jegan@tektutor.org:~/git-demo$ echo "Line 1" >> file1.txt
jegan@tektutor.org:~/git-demo$ git commit -am "Added Line 1"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main 5800304] Added Line 1
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ echo "Line 2" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added Line 2"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main 872e2c3] Added Line 2
 1 file changed, 1 insertion(+)
	
jegan@tektutor.org:~/git-demo$ git log --oneline
872e2c3 (HEAD -> main) Added Line 2
5800304 Added Line 1
38f4992 Initial commit.
jegan@tektutor.org:~/git-demo$ git status
On branch main
nothing to commit, working tree clean
	
jegan@tektutor.org:~/git-demo$ git checkout -b dev-1.0
Switched to a new branch 'dev-1.0'
	
jegan@tektutor.org:~/git-demo$ ls
file1.txt
	
jegan@tektutor.org:~/git-demo$ cat file1.txt 
Line 1
Line 2
	
jegan@tektutor.org:~/git-demo$ echo "Line 3" >> file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Added Line 3 in dev-1.0 branch"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[dev-1.0 5366320] Added Line 3 in dev-1.0 branch
 1 file changed, 1 insertion(+)
	
jegan@tektutor.org:~/git-demo$ echo "Line 4" >> file1.txt 
	
jegan@tektutor.org:~/git-demo$ git commit -am "Added Line 4 in dev-1.0 branch"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[dev-1.0 66d6ed7] Added Line 4 in dev-1.0 branch
 1 file changed, 1 insertion(+)
	
jegan@tektutor.org:~/git-demo$ git log --oneline
	
66d6ed7 (HEAD -> dev-1.0) Added Line 4 in dev-1.0 branch
5366320 Added Line 3 in dev-1.0 branch
872e2c3 (main) Added Line 2
5800304 Added Line 1
38f4992 Initial commit.

jegan@tektutor.org:~/git-demo$ git checkout main
Switched to branch 'main'
	
jegan@tektutor.org:~/git-demo$ git log --oneline
872e2c3 (HEAD -> main) Added Line 2
5800304 Added Line 1
38f4992 Initial commit.
	
jegan@tektutor.org:~/git-demo$ git cherry-pick 5366320
[main 0174cbc] Added Line 3 in dev-1.0 branch
 Date: Tue Jun 27 13:01:42 2023 +0530
 1 file changed, 1 insertion(+)
	
jegan@tektutor.org:~/git-demo$ git status
On branch main
nothing to commit, working tree clean
	
jegan@tektutor.org:~/git-demo$ git log --oneline
0174cbc (HEAD -> main) Added Line 3 in dev-1.0 branch
872e2c3 Added Line 2
5800304 Added Line 1
38f4992 Initial commit.
</pre>

## Git Stash

- Let's say you are working in a medium priority bug fix. You are half way completed the buge fix.
- QA team now reported a critical show stopper issue
- With the help of stash you can temporarily store/park your incomplete code changes in your local repo.  Once you are done with the critical fix, you may r\sume working on the medium poriority issue 

## Lab - Git stash
<pre>
jegan@tektutor.org:~/git-demo$ git init
Initialized empty Git repository in /home/jegan/git-demo/.git/
jegan@tektutor.org:~/git-demo$ touch file1.txt
jegan@tektutor.org:~/git-demo$ git add .
jegan@tektutor.org:~/git-demo$ git commit -m "Initial commit."
[main (root-commit) 5fffdd4] Initial commit.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1.txt
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Implemented new feature 1"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main b1a46c4] Implemented new feature 1
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Implemented new feature 2"
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
[main f17dad8] Implemented new feature 2
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ git log --oneline
f17dad8 (HEAD -> main) Implemented new feature 2
b1a46c4 Implemented new feature 1
5fffdd4 Initial commit.
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
jegan@tektutor.org:~/git-demo$ git stash --save BUG123
error: unknown option `save'
usage: git stash [push [-p|--patch] [-k|--[no-]keep-index] [-q|--quiet]
                 [-u|--include-untracked] [-a|--all] [-m|--message <message>]
                 [--] [<pathspec>...]]

    -k, --keep-index      keep index
    -p, --patch           stash in patch mode
    -q, --quiet           quiet mode
    -u, --include-untracked
                          include untracked files in stash
    -a, --all             include ignore files
    -m, --message <message>
                          stash message
    --pathspec-from-file <file>
                          read pathspec from file
    --pathspec-file-nul   with --pathspec-from-file, pathspec elements are separated with NUL character

jegan@tektutor.org:~/git-demo$ git stash save BUG123
warning: LF will be replaced by CRLF in file1.txt.
The file will have its original line endings in your working directory
Saved working directory and index state On main: BUG123
jegan@tektutor.org:~/git-demo$ git stash list
stash@{0}: On main: BUG123
jegan@tektutor.org:~/git-demo$ ls
file1.txt
jegan@tektutor.org:~/git-demo$ git status
On branch main
nothing to commit, working tree clean
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git commit -am "Fixed critical show-stopper issue BUG4354"
[main b3dae7e] Fixed critical show-stopper issue BUG4354
 1 file changed, 1 insertion(+)
jegan@tektutor.org:~/git-demo$ git log --oneline
b3dae7e (HEAD -> main) Fixed critical show-stopper issue BUG4354
f17dad8 Implemented new feature 2
b1a46c4 Implemented new feature 1
5fffdd4 Initial commit.
jegan@tektutor.org:~/git-demo$ git stash list
stash@{0}: On main: BUG123
jegan@tektutor.org:~/git-demo$ git stash pop
Auto-merging file1.txt
CONFLICT (content): Merge conflict in file1.txt
The stash entry is kept in case you need it again.
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git status
On branch main
Unmerged paths:
  (use "git restore --staged <file>..." to unstage)
  (use "git add <file>..." to mark resolution)
	both modified:   file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
jegan@tektutor.org:~/git-demo$ vim file1.txt 
jegan@tektutor.org:~/git-demo$ git add .
jegan@tektutor.org:~/git-demo$ git commit -m "Fixed medium priority issue BUG56456"
[main 5d0fb6d] Fixed medium priority issue BUG56456
 1 file changed, 3 insertions(+)
jegan@tektutor.org:~/git-demo$ git status
On branch main
nothing to commit, working tree clean
jegan@tektutor.org:~/git-demo$ git log --oneline
5d0fb6d (HEAD -> main) Fixed medium priority issue BUG56456
b3dae7e Fixed critical show-stopper issue BUG4354
f17dad8 Implemented new feature 2
b1a46c4 Implemented new feature 1
5fffdd4 Initial commit.	
</pre>
