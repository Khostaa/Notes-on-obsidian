# Branches
- Branch - individual version of a repo
- Git uses `branches` to systematically track multiple versions of files
- In each branch:
	- some files might be the same
	- others might be different
	- some may not exist at all
- each branch should have a Particular purpose
	- developing a new feature
	- debugging an error
Default branch = `main`
- allows multiple developers to work on a project simultaneously.
- Git makes it easy to compare a repo's state between branches, and to combine contents between branches, allowing us to push new features to our live software. Generally, each branch should have a specific purpose.
- usually used for feature development. new branch for each feature
## identifying branches
- listing all branches
```git
git branch
: * means current branch
```
- switching between branches
```git
git switch main
: switched to branch 'main'
```
- creating new branch
```git
git branch speed-test

`Move to 'speed-test' branch`
git switch speed-test
```
- creating a new branch called `speed-test` and switch to it
```git 
git switch -c speed-test
```
## Modifying and Comparing branches
![[git diff.png]]
- comparing two branches `main` and `summary-statistics`
```git
git diff main summary-statistics
```
- Press `space` to navigate through output and `q` to exit
- Show existing branches
```git
git branch
```
- Renaming a branch `feature_dev` to `chatbot`
- To rename a branch, we use the git branch command with the -m flag.
```git
git branch -m old_name new_name
git branch -m feature_dev chatbot
```
- Deleting a branch once we're finished with them
- Delete `chatbot` branch with `-d` flag
```git
git branch -d chatbot
```
- if `chatbot` hasn't been merged to `main`, above code will produce an error
- In such case, Delete with `-D` flag
```git
git branch -D chatbot
```
- Difficult, but not impossible, to recover deleted branches
- Be sure we don't need the branch any more before deleting!
## Merging branches
- each branch should have a Particular purpose
	- developing a new feature
	- debugging an error
- Once the task is complete, we incorporate the changes into production
	- Typically ` main` branch - "ground truth"

- When merging two branches:
	- the last commits from each branch are called **parent commits**
	- source—the branch we want to merge **from**
	- destination—the branch we want to merge **into**
- When merging ai-assistant into main:
	- ai-assistant = source
	- main = destination
- Move to `destination` branch:
```git
git switch main
or
git checkout main
```
- ` git merge source`
- From `main`, to merge `ai-assistant` into `main`:
```git
git merge ai-assistant
```
- from another branch: `git merge source destination`
```git
git merge ai-assistant main
```
## Conflicts
- inability to resolve differences in the contents of one or more files between branches.
- When?
	- edit the same file in two branches
	- try to merge
	- git doesn't know what version to keep
	- conflict!
- For the example below, there are conflicting versions of `README.md` in `documentation` branch and `main` branch
### Merging 
- from the *main* branch
```git
git merge documentation
# output - conflict arises
```
- opening the file
```terminal
nano README.md
```
![[git conflict syntax.png]]
- resolve the conflict
- Save: `Ctrl + o`, then `Enter`
- Exit: `Ctrl + x`
- merging the branches
```git
git add README.md
git commit -m "Resolving README.md conflict"
git merge documentation
```
> Avoid Editing the same file in multiple branches

## Introduction to remotes
- a repo stored in the cloud.
- everything is backed up
- collaboration, regardless of location
### Cloning a repo
- Repo copies on our local computer = local remotes
- Making copies = cloning
```git
git clone path-to-project-repo
```
- cloning a local project
```git
git clone /home/george/repo
```
- cloning an naming a local repo
```git
git clone /home/george/repo new_repo
```
- Remote Repos are generally stored in an online hosting service.
- e.g: GitHub, BitBucket, or GitLab
- clone a remote repo on to our local repo
```git
git clone URL
# example
git clone https://github.com/datacamp/project
```
### Identifying a remote
- When cloning a repo
	- git remembers where the original was
- Git stores a remote *tag* in the new repo's configuration
- List all remotes associated with repo
```git
git remote
```
- getting more information
```git
git remote -v
```
### Creating a remote
- when cloning, Git will automatically name the remote *origin*
```git
git remote add name URL
```
- create a remote called *geroge*
```git
git remote add george https://github.com/george_datacamp/repo
```
- defining remote name is useful for merging
## Collaborating on Git projects
- If several people are collaborating on a project then they will access the remote, work locally, save files, and synchronize their changes between the remote and local repos. 
- This means that the remote repo should be the project's source of truth, where the latest versions of files that are not drafts can be located.
### Fetching from a remote
- Fetch from the *origin* remote
```git
git fetch origin
```
- this Fetch all remote branches from the remote into the local repo.
- Might create new local branches if they only existed in the remote
- Doesn't merge the remote's contents into local repo
### Fetching a remote branch
- Fetch only the *orgin* remote's *main* branch.
```git
git fetch origin main
```
- The output displays the URL or path we are fetching from, the branch, and that we are fetching the HEAD, or last commit.
### Synchronizing content
- Merge `origin` remote's default branch (`main`) into the local repo's current branch
```git
git remote origin
```
### Pulling from a remote
- local and remote synchronization is a common workflow
- git simplifies this process for us!
- Fetch and merge from the remote's default (`main`) into the local repo's current branch
```git
git pull orgin
```
### Pulling a remote branch
- Pull from the `origin` remote's `dev` branch
```git
git pull origin dev
```
- still merges into the local branch we are located in!
### Git pull output
```git
git pull origin
```
> Note that if we have been working locally and not yet committed our changes, then Git won't allow us to pull from a remote. We are instructed to commit our changes and told that the pull command was aborted. Therefore, it's important to save our work locally before we pull from a remote.
- important to save locally before pulling from a `remote`

### Pushing to remotes
#### git push
- save changes locally first
- Push into `remote` from `local_branch`
```git
git push remote local_branch
```
- Push changes into `origin` from the local repo's `main` branch
```git
git push origin main
```

![[pushpull workflow.png]]
- Pushing `main` to the remote before pulling
```
git push origin main
```
- to avoid a conflict
	- pull from the remote first
```git
	git pull origin main
```

- Pulling without editing
```git
git pull --no-edit origin main
```

### Pushing a new local branch
- working in `hotfix` branch locally
- `hotfix` does not exist in the remote
- `hotfix` only exist locally
- creating a new remote branch
```git
git push origin hotfix
```