# Day 1

## 📌 Installing Git in Windows
<pre>
https://gitforwindows.org/
</pre>

## 📌 Installing Git in Ubuntu Linux Distribution
<pre>
sudo add-apt-repository ppa:git-core/ppa 
sudo apt update
sudo apt install git
</pre>

## 📌 Installing Git in RedHat Family Linux Distributions
```
sudo yum install -y epel-release && sudo yum -y install git
sudo dnf install git
```

## 🔖 How to clone this repository from Git Bash CLI ?
```
cd ~
git clone https://github.com/tektutor/git-china-june2023-batch1.git
cd git-china-june2023-batch1
```

## 📎 What is a Git repository ?
- a folder that is being tracked by your Git server
- it is a version controlled folder
- Git tracks all changes done to files/folder within the repository
- the history/version of changes done to files/folders within the repository are tracked by Git

## 📎 What is a Version Control System (VCS) ?


## 📎 What is a Local Version Control System (LVCS) ?
- you could install some Local Version Control system on your laptop/desktop

### Advantages
- only you will have access to your code repository
- you will have unrestricted access to your code repository
- you could work offline

### Disadvantages
- multiple team members can't collaborate
- single point failure, in case your code repository gets corrupted due to OS crash or some issue on your local system, the entire will be lost

## 📎 What is a Centralized Version Control System (CVCS) ?
- client/server architecture
- The CVCS software is installed on a Centralized Physical Server that is accessible to all team members within an Organization
- Each Team members that works in a project will have some kind of client software installed on their local laptop/desktop

## Advantages
- could control access to the source code repository, i.e different users having different types of access
- helps multiple team members work in a source code repository simultaneously

## Drawbacks
- Single point of failure, i.e your centralized server goes down or there is a network outage
- can't work offline

## 📎 What is a Distributed Version Control System (DVCS) ?
- it doesn't follow client/server architecture

- Examples
  - Git/GitHub,etc
 
#### Advantages
- all benefits of CVCS is there in DVCS too
- we could work offline without any need for network/internet
- supports working offline, pretty much all Git features all possible in a disconnected mode
- the only time we need to be connected to the remote GitHub server is either you wish to pull latest changes from remote server to local or when you wish merge your changes done locally to the remote server

## 📎 Pros and Cons of LVCS

#### Advantages

#### Disadvantages


## 📎 Pros and Cons of CVCS

#### Advantages

#### Disadvantages

## 📎 Pros and Cons of DVCS

#### Advantages

#### Disadvantages

## 📎 What is Git Bash ?


# Git Commands ( Try these commands on your Git Bash )

## Checking Git tool version
```
git --version
```

Expected output
<pre>
jegan@tektutor.org:~$ <b>git --version</b>
git version 2.34.1
</pre>


## Creating a local empty git repository
```
cd ~
mkdir git-demo
cd git-demo

git init
```

Expected output
<pre>
jegan@tektutor.org:~$ cd ~
jegan@tektutor.org:~$ pwd
/home/jegan
jegan@tektutor.org:~$ mkdir git-demo
jegan@tektutor.org:~$ ls
Documents           Templates
Downloads           Videos
<b>git-demo</b>     Pictures
Public
Desktop              Music
jegan@tektutor.org:~$ cd git-demo/
jegan@tektutor.org:~/git-demo$ ls
jegan@tektutor.org:~/git-demo$ ls -lha
total 8.0K
drwxrwxr-x  2 jegan jegan 4.0K Jun 19 11:35 .
drwxr-x--- 38 jegan jegan 4.0K Jun 19 11:35 ..
jegan@tektutor.org:~/git-demo$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /home/jegan/git-demo/.git/
jegan@tektutor.org:~/git-demo$ ls
jegan@tektutor.org:~/git-demo$ ls -lha
total 12K
drwxrwxr-x  3 jegan jegan 4.0K Jun 19 11:36 .
drwxr-x--- 38 jegan jegan 4.0K Jun 19 11:35 ..
drwxrwxr-x  7 jegan jegan 4.0K Jun 19 11:36 .git
jegan@tektutor.org:~/git-demo$ tree .git
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── push-to-checkout.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

9 directories, 17 files
</pre>


## Configuring your local Git

The configuration changes can be stored in 3 differents levels
1. System wide ( the config changes are applied for all users in the OS )
2. Global - the config changes are applied for all code repositories a particular user is working on
3. Local - the config changes are applied to a particular code repository used by a single user

Let's perform some basic configuration on the global level
```
git config --global user.name "Jeganathan Swaminathan"
git config --global user.email "mail2jegan@gmail.com"
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ <b>git status</b>
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
jegan@tektutor.org:~/git-demo$ git config --global user.name "Jeganathan Swaminathan"
jegan@tektutor.org:~/git-demo$ git config --global user.email "maiegan@gmail.com"

jegan@tektutor.org:~/git-demo$ git config --list
credential.helper=cache --timeout=9999999999
user.name=Jeganathan Swaminathan
user.email=maiegan@gmail.com
pull.rebase=false
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true

jegan@tektutor.org:~/git-demo$ git config --global user.email "mail2jegan@gmail.com"
jegan@tektutor.org:~/git-demo$ git config --list
credential.helper=cache --timeout=9999999999
user.name=Jeganathan Swaminathan
user.email=mail2jegan@gmail.com
pull.rebase=false
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
</pre>

## Configuring your preferred editor in local git environment
```
git config --global core.editor "vim"
git config --list
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git config --list
credential.helper=cache --timeout=9999999999
user.name=Jeganathan Swaminathan
user.email=mail2jegan@gmail.com
pull.rebase=false
core.editor=vim
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
</pre>

## Removing global configurations
The global git configurations are stored under user home .gitconfig file

```
git config --unset --global user.email
git config --unset --global user.name
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git config --list
credential.helper=cache --timeout=9999999999
user.email=mail2jegan@gmail.com
pull.rebase=false
core.editor=vim
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true

jegan@tektutor.org:~/git-demo$ git config --unset --global user.email
jegan@tektutor.org:~/git-demo$ git config --list
credential.helper=cache --timeout=9999999999
pull.rebase=false
core.editor=vim
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
</pre>

## Saving the git config details on the local scope. These config changes are only applied to a single git repo

The local git configurations are stored within in the local git repo folder at the below path
./git/config

```
git config --local user.name "Jeganathan Swaminathan"
git config --local user.email "mail2jegan@gmail.com"
git config --local -l
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git config --local user.name "Jeganathan Swaminathan"
jegan@tektutor.org:~/git-demo$ git config --local user.email "mail2jegan@gmail.com"

jegan@tektutor.org:~/git-demo$ git config --local -l
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
user.name=Jeganathan Swaminathan
user.email=mail2jegan@gmail.com
jegan@tektutor.org:~/git-demo$ ls -lha
total 12K
drwxrwxr-x  3 jegan jegan 4.0K Jun 19 11:36 .
drwxr-x--- 38 jegan jegan 4.0K Jun 19 12:17 ..
drwxrwxr-x  7 jegan jegan 4.0K Jun 19 12:17 .git
jegan@tektutor.org:~/git-demo$ tree .git
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── push-to-checkout.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

9 directories, 17 files
jegan@tektutor.org:~/git-demo$ cat .git/config
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[user]
	name = Jeganathan Swaminathan
	email = mail2jegan@gmail.com
</pre>

## Configuring your git in case you are behind proxy server
```
git config --global http.proxy https://your-proxy-server:8080
git config --global http.proxy https://user-name:password@your-proxy-server:8080
git config --global -l
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git config --global http.proxy https://your-proxy-server:8080
jegan@tektutor.org:~/git-demo$ git config --global http.proxy
https://your-proxy-server:8080
jegan@tektutor.org:~/git-demo$ git config --global -l
credential.helper=cache --timeout=9999999999
pull.rebase=false
core.editor=vim
http.proxy=https://your-proxy-server:8080
jegan@tektutor.org:~/git-demo$ git config --global http.proxy https://user-name:password@your-proxy-server:8080
</pre>


## Finding current status of your local git repo
```
git status
touch cars.txt
ls -l
cd ~/git-demo
git status
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ touch cars.txt

jegan@tektutor.org:~/git-demo$ ls -l
total 0
-rw-rw-r-- 1 jegan jegan 0 Jun 19 12:46 cars.txt

jegan@tektutor.org:~/git-demo$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	cars.txt

nothing added to commit but untracked files present (use "git add" to track)
</pre>

## Staging our changes in our local git repo
```
git add cars.txt
git status
```

Expected output
<pre>
jegan@tektutor.org:~/git-demo$ git add cars.txt 

jegan@tektutor.org:~/git-demo$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   cars.txt
  </pre>

## Removing files from the staging are 
```
git rm --cached cars.txt
git status
```

<pre>
jegan@tektutor.org:~/git-demo$ git rm --cached cars.txt 
rm 'cars.txt'

jegan@tektutor.org:~/git-demo$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	cars.txt

nothing added to commit but untracked files present (use "git add" to track)
</pre>

## Staging multiple files in our local git repo
```
git add *
git status
```
   
jegan@tektutor.org:~/git-demo$ git add *

jegan@tektutor.org:~/git-demo$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   cars.txt
</pre>
