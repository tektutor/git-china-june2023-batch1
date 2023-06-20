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
```

The possible specifiers
<pre>
%H - Full length commit Hash
%h - shorter commit hash
%an- author name
%ae - author email
%s - Commit message
</pre>
