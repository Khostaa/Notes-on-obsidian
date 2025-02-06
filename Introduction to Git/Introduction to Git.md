# What is version control?
- processes and systems to manage changes to files, programs, and directories.
## What can version control do?
- useful for anything that:
	- changes over time
	- needs to be shared
## What can version control do?
- track files in different states
- combine different versions of files
- Identify a particular version
- Revert changes

# Introducing Git
- popular version control system for software development and data projects.
- open source
- scalable
## Benefits of Git
- Git stores everything, so nothing is lost
- we can compare files at different times
- see what changes were made, by who, and when

## Using Git
- Git commands are run on the shell, also known as the terminal
- The shell:
	- is a program for executing commands
	- can be used to easily preview or inspect files and directories
### Useful terminal commands
directory - folder
- pwd - present working directory
- ls - what's in our current directory
- cd - changing 

### Checking git version
```terminal
git --version
```
### Creating repos
#### What is git repo?
- Git repo = directory containing files and sub-directories, and Git storage (.git folder)
> Do not edit .git!

#### Why make a repo?
- systematically track versions
- revert to previous versions
- compare versions at different points in time
- collaborate with colleagues
#### Creating a new repo
```terminal
#  creating new git repo
git init repo_name

# converting existing directory into git repo
git init

cd git_repo

# check status of repo
git status
```

#### Nested repositories
- Don't create a Git repo inside another Git repo
	- known as nested repos
- There will be two **.git** directories
- which **.git** directory should be updated? - git gets confused

## The Git workflow
- edit and save files on our computer
- Add file(s) to the Git staging area
	- Tracking what has been modified
- Commit the files
	- Git takes a snapshot of the files at the point in time
	- Allows us to compare and revert files

### Adding to staging area
- adding a single file
```git
git add README.md
```
- adding all modified files
```git
git add .
```
- "." means all files in the current directory and sub-directories
### Making a commit
```git
git commit -m "Addign a README"
```
- "-m" allows a log message without opening a text editor
- adding only "git commit" - opens a text editor where commit message has to be written and file has to be saved.
- Log message is useful for reference
- Best practice = short and concise

# Viewing the version history
## The Commit Structure
Git commits has three parts:
1. Commit
	1. contains the metadata - author, log message, commit time
2. Tree
	1. tracks the names and locations of files and directories in the repo
	2. like a dictionary - mapping keys to files/directories
3. Blob
	1. Binary Large OBject
	2. may contain any kind of data
	3. a compressed snapshot of a file's contents
![[visualizing the commit structure.png]]
## Git hash
- 40-character string of number and letters
- git produces it using a  pseudo-random number generator called a hash function
- Hashes enable Git to share data efficiently between repos.
- if two files are same, their hashes will be the same
- Therefore, Git can tell what information needs to be saved in which location by comparing hashes rather than entire files.
## Git log
- view commit information using
```git
git log
```
- shows commits from newest to oldest
- it will show commit hash, author, date, and commit message.
-  If the output doesn't fit in the terminal window, a colon will be at the end, indicating more commits.
- We can see more by pressing the space bar.
- To exit the log, we can press q and return to the terminal.

## Version history tips and tricks
- Larger project = more commits = larger output
### Restricting the number of commits
- no. of commits displayed can be restricted using " - ":
```terminal
# restrict to 3 most recent commits
git log -3
```
### Restricting the file
- to only look at the commit history of one file
```terminal
# show only commits done to report.md file
git log report.md
```

### Combining techniques
```terminal
cd data
git log -2 mental_health_survey.csv
```

### Customizing the date range
- Restrict *git log* by date:
```terminal
git log --since='Month Day Year'
```
- where month is a three-letter abbreviation, day is one or two digits, and year is four digits.
- e.g: commits since 2nd April 2024:
```terminal
git log --since='Apr 2 2024'
```
- commits between 2nd and 11th April:
```terminal
git log --since='Apr 2 2024' --until='Apr 11 2024'
```
- The since and until flags are very flexible in the date and time formatting that they accept.
![[formats for since and until.png]]
### Finding a particular commit
 ```terminal
 git log
```
- only need the first 8 to 10 characters of the hash
```terminal
git show c27fa856
```
- The output displays the log entry for that commit at the top, followed by a diff output showing changes between the file in that commit and the current version in the repo.

# Comparing versions
```terminal
- Difference between versions
git diff 

# compare last committed version with latest version not in the staging area
git diff report.md

# add report.md to staging area
git add report.md

# compare last committed version of report.md with the version in the staging area
git diff --staged report.md

# compare all staged files to versions in the last commit
git diff --staged
```

## Comparing two commits
- find the commit hashes
```terminal
git log
```
- compare them
```terminal
git diff hash1 hash2 
```
- what changed from first hash to second hash
	- put most recent hash second
- state in latest commit = HEAD
- compare second most recent with the most recent commit
```terminal
git diff HEAD~1 HEAD
```
![[comparing versions.png]]

# Restoring and reverting files
## Reverting files
- restoring a repo to the state prior to the previous commit
```terminal
git revert
```
- reinstates previous versions and makes a commit
- restores all files updated in the given commit
- need to provide reference to commit hash or head to undo last commits.
	- HEAD~1 : second most last commit

```terminal
git revert HEAD

Save: Ctrl + 0 then, Enter
Exit: Ctrl + X
```
### avoid opening the text editor
```terminal
git revert --no-edit HEAD
```

### Revert without committing (bring files into the staging area)
```terminal
git revert -n HEAD
# -n means no commit
```

- **git revert** works on commits, not individual files
- to revert a single file:
	- git checkout
	- use commit hash or *HEAD* syntax
```terminal
git checkout HEAD~1 -- filename
```
### checking the checkout
```terminal
git status
```
### Making a commit
```terminal
git commit -m "message here"
```

## Unstaging a file
### Single file
```terminal
git restore --staged filename
```
- Edit the file
	- git add filename
	- git commit -m "message"
### all files
```terminal
git restore --staged
```
![[restoring and reverting files.png]]