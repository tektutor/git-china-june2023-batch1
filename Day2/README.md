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
