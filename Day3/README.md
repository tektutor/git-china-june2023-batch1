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


