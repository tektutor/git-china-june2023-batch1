# Day 2

## Removing a file from staging are but retain in the working directory
```
git rm --cached file2.txt
```

## Removing a file from staging and delete it from working directory
```
git rm -f file2.txt
```

## Different types of log commands you may find it useful
```
git log -p -2
git log --stat
git log --pretty=oneline
git log --pretty=short
git log --pretty=full
git log --pretty=fuller
git log --pretty=format:"%h - %an %ar %s"

git log --pretty=format:"%h %s" --graph
git log --since=2.weeks
git log --path path-of-the-file
git log --oneline --decorate

git log --pretty="%h - %s" --author="Jeganathan Swaminathan" --since="2023-06-18" --before="2023-06-21"
```

The possible specifiers
<pre>
%H - Full length commit Hash
%h - shorter commit hash
%an- author name
%ae - author email
%s - Commit message
</pre>

## Lab - Understanding Git Diff

Finding changes done on unstaged files
```
git diff
```

Finding changes that will go in the next commit
```
git diff --staged
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git diff
jegan@tektutor.org:~/git-demo$ ls
cars.txt  file2.txt  file3.txt
jegan@tektutor.org:~/git-demo$ vim cars.txt
jegan@tektutor.org:~/git-demo$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   cars.txt

no changes added to commit (use "git add" and/or "git commit -a")
jegan@tektutor.org:~/git-demo$ git diff
diff --git a/cars.txt b/cars.txt
index dffa255..c2af84c 100644
--- a/cars.txt
+++ b/cars.txt
@@ -1 +1,2 @@
 BMW X3
+Audi A6
jegan@tektutor.org:~/git-demo$ git add cars.txt 
    
jegan@tektutor.org:~/git-demo$ git diff --staged
diff --git a/cars.txt b/cars.txt
index dffa255..c2af84c 100644
--- a/cars.txt
+++ b/cars.txt
@@ -1 +1,2 @@
 BMW X3
+Audi A6
</pre>

## Lab - Recommended configuration on Windows machines
```
git config --global core.autocrlf true
```

The above configuration ensures the same control characters used in Windows machines so that the other unix/linux/mac users won't see conflicting formatting characters. This should help avoid the CRLF warning that windows users might get.

## ⛹️‍♂️ Lab - Discard changes done in the working directory on a unstaged file

Modify the cars.txt but dont' stage it before you try the restore
```
echo "Mahindra Bolerao" > cars.txt
cat cars.txt
git status
git restore cars.txt
git status
cat cars.txt
```

## ⛹️‍♂️ Lab - Restore changes done in the recent commit

Git restores requires an additional commit.

Assume the cars.txt file has just the below entries
<pre>
BMW X3
Audi A6
</pre>

```
echo "Mahindra XUV" > cars.txt
cat cars.txt
git status
git commit -am "Added Mahindra XUV"
git status
git log --oneline --decorate
git restore --source c0e1f22 cars.txt
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git log --oneline --decorate
f63cb89 (HEAD -> main) Added Mahindra Bolero
c0e1f22 Undone the changes made to cars.txt
8f3f7d8 Removed Audi Q7
61e2f52 Added Audi Q7
e0ce153 Added BMW X3
a9d2c51 Deleted file2.txt from local repo.
43de063 Initial commit.
jegan@tektutor.org:~/git-demo$ git restore --source c0e1f22 cars.txt
jegan@tektutor.org:~/git-demo$ ls
cars.txt  file2.txt  file3.txt
jegan@tektutor.org:~/git-demo$ cat cars.txt 
BMW X3
Audi A6

jegan@tektutor.org:~/git-demo$ git log --oneline --decorate
f63cb89 (HEAD -> main) Added Mahindra Bolero
c0e1f22 Undone the changes made to cars.txt
8f3f7d8 Removed Audi Q7
61e2f52 Added Audi Q7
e0ce153 Added BMW X3
a9d2c51 Deleted file2.txt from local repo.
43de063 Initial commit.
jegan@tektutor.org:~/git-demo$ ls
cars.txt  file2.txt  file3.txt
jegan@tektutor.org:~/git-demo$ cat cars.txt 
BMW X3
Audi A6
jegan@tektutor.org:~/git-demo$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   cars.txt

no changes added to commit (use "git add" and/or "git commit -a")

jegan@tektutor.org:~/git-demo$ git commit -am "Reverted or removed the Mahendra Bolero from cars.txt"
[main 5961c98] Reverted or removed the Mahendra Bolero from cars.txt
 1 file changed, 1 deletion(-)

jegan@tektutor.org:~/git-demo$ git log --oneline --decorate
5961c98 (HEAD -> main) Reverted or removed the Mahendra Bolero from cars.txt
f63cb89 Added Mahindra Bolero
c0e1f22 Undone the changes made to cars.txt
8f3f7d8 Removed Audi Q7
61e2f52 Added Audi Q7
e0ce153 Added BMW X3
a9d2c51 Deleted file2.txt from local repo.
43de063 Initial commit.
</pre>

## If you wish to modify the recent commit comment or missed to commit some additional files part the commit but would like to add those changes in the same commit
```
git commit --amend
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git commit --amend
[main d68ef7e] Added BMW X3
 Date: Tue Jun 20 13:12:58 2023 +0530
 1 file changed, 1 insertion(+)

jegan@tektutor.org:~/git-demo$ git log --oneline --decorate
d68ef7e (HEAD -> main) Added BMW X3
88f39c4 Added BMW X2
73cb3ee Added BMW X1
32187fd Initial commit
</pre>


