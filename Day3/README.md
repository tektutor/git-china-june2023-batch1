# Day 3

## Git Commands single line description

<pre>
git init - this command is used to create new local empty repository
git status - will display the current state of your working repository/tree
git add - is used to stage the code changes before it can be commited into the code repository
git commit - is used to check-in the code changes into the local git repo
git diff - is used to compare the changes between two revisions/version of a file in the code repo
git log - is used to see the historical changes a file(s) underwent in a code repo
git commit ammend - is used to rectify errors in commit message or adding a missing file to existing commit
git restore - is used to discard changes done, this will preserve the commit history by allowing to revert changes in a new commit
git reset - is also used to discard changes done but without making an extra commit.  This would modify the commit history
</pre>

# Git Reset

Supports two types of Resets
1. Soft - will discard the code changes done in a commit but preserves the changes in the staging area
2. Hard - will discard the code changes done in a commit but also removes the changes in the local file system and staging area


## ⛹️‍♀️ Lab - Git soft reset
The soft reset will remove the changes done in the code repo but retains those code changes in the staging area. Both soft and hard resets will modify the commit history in the code repository, hence commit that was reset is lost permanently. This is not recommended in case the code is already pushed to GitHub or similar code repository, as other developers might depend on those changes.

The alternate to reset is using restore.
```
cd ~/git-demo
rm -rf .git
rm *
git init
touch cars.txt
git add cars.txt
git commit -m "Initial commit"

echo "Car 1" > cars.txt
git commit -am "Added Car 1"

echo "Car 2" >> cars.txt
git commit -am "Added Car 2"

echo "Car 3" >> cars.txt
git commit -am "Added Car 3"

echo "Car 4" >> cars.txt
git commit -am "Added Car 4"

echo "Car 5" >> cars.txt
git commit -am "Added Car 5"

git log --oneline

git reset --soft 

```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git log --oneline
ac2cac5 (HEAD -> main) Added Car 5
f1c9eff Added Car 4
ea4fd61 Added Car 3
1714c98 Added Car 2
0c339fa Added Car 1
232db7f Initial commit.
jegan@tektutor.org:~/git-demo$ cat cars.txt 
Car 1
Car 2
Car 3
Car 4
Car 5
jegan@tektutor.org:~/git-demo$ git reset --soft f1c9eff
jegan@tektutor.org:~/git-demo$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   cars.txt

jegan@tektutor.org:~/git-demo$ cat cars.txt 
Car 1
Car 2
Car 3
Car 4
Car 5
jegan@tektutor.org:~/git-demo$ git restore --staged cars.txt
jegan@tektutor.org:~/git-demo$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   cars.txt

no changes added to commit (use "git add" and/or "git commit -a")  
</pre>

## ⛹️‍♀️ Lab - Git hard reset

Unlike the soft reset, the hard reset will remove from code repo and remove those changes from staging area and the file system.

```
git log --oneline
git reset --hard 1714c98  # All code commits after this commit id will be removed permanently
git log --oneline
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git log --oneline
f1c9eff (HEAD -> main) Added Car 4
ea4fd61 Added Car 3
1714c98 Added Car 2
0c339fa Added Car 1
232db7f Initial commit.

jegan@tektutor.org:~/git-demo$ git reset --hard 1714c98            
HEAD is now at 1714c98 Added Car 2

jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main) Added Car 2
0c339fa Added Car 1
232db7f Initial commit.
</pre>

## Git restore vs Git reset

#### Git restore
- will preserve the past commit history
- the code that you wanted to discard will removed and then committed as a new commit on top of existing commit id
- hence this is considered safer
- the only drawback is, it requires an additional commit to undo the changes

#### Git reset
- will modify the past commit history
- once the reset is done, we will permanently lose the code changes
- the drawback is, you will lose the commit history
- the advantage is, it looks neat as no one will see the faulty commits

In general, use of restore is recommended over the reset.  But using reset is recommended in case the code that is reset isn't published yet to the Git remote repo ( ie - GitHub or similar remote repo )

## Git Tags

Git supports two types of tags
1. Lightwight tags - this will not require additional objects stored in .git folder, hence this is lightweight
2. Annotated tags - this will create a separate object for tags, but this is recommended

## ⛹️‍♀️ Lab - Creating lightweight tags in Git
```
cd ~/git-demo
git log --oneline

git tag v0.1 232db7f  # Creates a lightweight tag
git tag v0.2 0c339fa  # Creates a lightweight tag
git tag v0.3 1714c98  # Creates a lightweight tag

git log --oneline
git tag # List the tags
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main) Added Car 2
0c339fa Added Car 1
232db7f Initial commit.
	
jegan@tektutor.org:~/git-demo$ git tag v0.1 232db7f
jegan@tektutor.org:~/git-demo$ git tag v0.2 0c339fa
jegan@tektutor.org:~/git-demo$ git tag v0.3 1714c98

jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main, tag: v0.3) Added Car 2
0c339fa (tag: v0.2) Added Car 1
232db7f (tag: v0.1) Initial commit.
	
jegan@tektutor.org:~/git-demo$ git tag
v0.1
v0.2
v0.3
</pre>

## ⛹️‍♀️ Lab - Deleting tags
```
git log --oneline

git tag -d v0.1
git tag -d v0.2
git tag -d v0.3

git log --oneline

git tag
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git tag -d v0.1
Deleted tag 'v0.1' (was 232db7f)
jegan@tektutor.org:~/git-demo$ git tag -d v0.2
Deleted tag 'v0.2' (was 0c339fa)
jegan@tektutor.org:~/git-demo$ git tag -d v0.3
Deleted tag 'v0.3' (was 1714c98)
jegan@tektutor.org:~/git-demo$ git tag

jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main) Added Car 2
0c339fa Added Car 1
232db7f Initial commit.
</pre>

## ⛹️‍♀️ Lab - Git describe
```
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main, tag: v0.3) Added Car 2
0c339fa (tag: v0.2) Added Car 1
232db7f (tag: v0.1) Initial commit.
jegan@tektutor.org:~/git-demo$ git tag
v0.1
v0.2
v0.3
	
jegan@tektutor.org:~/git-demo$ git describe v0.1
v0.1
	
jegan@tektutor.org:~/git-demo$ git describe -h
usage: git describe [<options>] [<commit-ish>...]
   or: git describe [<options>] --dirty

    --contains            find the tag that comes after the commit
    --debug               debug search strategy on stderr
    --all                 use any ref
    --tags                use any tag, even unannotated
    --long                always use long format
    --first-parent        only follow first parent
    --abbrev[=<n>]        use <n> digits to display object names
    --exact-match         only output exact matches
    --candidates <n>      consider <n> most recent tags (default: 10)
    --match <pattern>     only consider tags matching <pattern>
    --exclude <pattern>   do not consider tags matching <pattern>
    --always              show abbreviated commit object as fallback
    --dirty[=<mark>]      append <mark> on dirty working tree (default: "-dirty")
    --broken[=<mark>]     append <mark> on broken working tree (default: "-broken")

jegan@tektutor.org:~/git-demo$ git describe --all --exact-match v0.1
tags/v0.1
jegan@tektutor.org:~/git-demo$ git describe --all --exact-match v0.3
tags/v0.3
jegan@tektutor.org:~/git-demo$ git describe --all --exact-match v0.2
tags/v0.2
	    
jegan@tektutor.org:~/git-demo$ git log --oneline
1714c98 (HEAD -> main, tag: v0.3) Added Car 2
0c339fa (tag: v0.2) Added Car 1
232db7f (tag: v0.1) Initial commit.
	    
jegan@tektutor.org:~/git-demo$ git describe --contains 0c339fa
v0.2^0	
</pre>
