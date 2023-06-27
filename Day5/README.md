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

