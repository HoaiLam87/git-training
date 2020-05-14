# Demo Project README

## Git config

```
[core]
  editor = notepad++.exe -multiInst -nosession
[user]
  name = <your-git-account-name>
  email = <your-email-linked-to-git-account>
[diff]
  tool = p4merge  [=> can download at https://www.perforce.com/downloads/visual-merge-tool]
[difftool "p4merge"]
  path = <directory-containing-installed-folder>/p4merge.exe
[difftool]
  promt = false
[merge]
  tool = p4merge
[mergetool "p4merge"]
  path = <directory-containing-installed-folder>/p4merge.exe
[mergetool]
  promt = false
[alias]
  hist = log --oneline --graph --decorate --all
[filter "lfs"]
  clean = git-lfs clean -- %f
  smudge = git-lfs smudge -- %f
  process = git-lfs filter-process
  required = true
```

## General commands

```
# Initiate new git project
  git init

# Add all files into tracked project
  git add .

# Commit all changes
# Optional: use -am "<commit message>" to stage and commit all tracked files with a message
  git commit

# Check status of current branch
  git status

# Set up remote
  git remote add <remote-name> <repo-address>

# Clone a repo into local machine
  git clone <remote-name> <repo-address> <optional: folder-name-if-needed>

# Stage changes (or add an untracked file)
  git add <.-if-add-all-changes>

# Publish changes
  git push <optional: remote-name> <optional: branch-name>

# Fetch changes
# Optional: use -p to fetch all reference changes
  git fetch -p <optional: remote-name> <optional: branch-name>

# Get new changes
# Option: use --all to pull all changes from all branches
  git pull <optional: remote-name> <optional: branch-name>

# Get summarised history of commits and branches
# Optional: use stash@{id} to get specific stash, get id from list of stashed changes
  git log --oneline -- graph --decorate --all stash@{id}
```

## Branches

```
# Create new branch
  git checkout -b <branch-name>

# Get all branches
  git branch -a

# Switch to a branch
  git checkout <branch-item>

# Delete a branch
  git branch -d <branch-name>
  git push <remote-name> :<branch-name>

# Merge branch
  git merge <branch-name>

# Prune stale reference of deleted branches
  git fetch -p
```

## Resolve conflict

```
# Check status of current branch
  git status

# Pull new changes to figure out conflict diversity
  git pull

# Run merge tool
  git mergetool

# Resolve conflicts on merge tool and save
# Commit the resolution
  git commit -m "<commit-message>"

# Removed all original files that are untracked
  rm *.orig

# Push new changes after resolving commit
  git push
```

## Reset remote

```
  git remote set-url <remote-name> <new-repo-address>
```

## Stash current changes for later

```
# Stash current changes (use -u or --include-untracked to stash untracked/new changes)
  git stash

# Stash current changes (use -u or --include-untracked to stash untracked/new changes)
# Optional: use save "<annotation>" to add a annotation for future reference
  git stash save "<annotation>"

# Get list of stashed changes
  git stash list

# Preview stashed changes for differences (use -p for more details)
# Optional: use stash@{id} to get specific stash, get id from list of stashed changes
  git stash show -p stash@{id}

# Take out stashed changes and delete stashed record
# Optional: use stash@{id} to get specific stash, get id from list of stashed changes
  git stash pop stash@{id}

# Take out stashed changes
# Optional: use stash@{id} to get specific stash, get id from list of stashed changes
  git stash apply stash@{id}

# Drop a stashed changes
# Optional: use stash@{id} to get specific stash, get id from list of stashed changes
  git stash drop stash@{id}

# Delete all stashes
  git stash clear
```

## Tags and release

```
# Get all commit logs
  git log --oneline

# Check tags
  git tag

# Create new lightweight tag on a branch
  git tag <tag-name> <branch-name>

# Create new annotated tag
  git tag -a <tag-name-maybe-version-number> -m "<tag-message>" <commit-id>

# Show tag information
  git show <tag-name>

# Push a tag to the repo
  git push <remote-name> <tag-name>

# Push all tags to the repo
  git push --tags

# Delete tags
  git fetch -p
  git tag -d <tag-name>
  git push <origin-name> :<tag-name>

# Create a floating tag
# It is recommended that deleting tag on GitHub repo before updating; if not, use force push, but it must be used with care so as not to cause confusion
  git tag -f <tag-name> <commit-id>
  git push --force <remote-name> <tag-name>

# To add a tag as a release, click "Add release note" on GitHub repo and add release information, tick "This is pre release" if the release is not official
# To delete a release, click "Delete" on release information on GitHub repo, the tag associated is still intact until deleted
```

## Comparing tags and pull request

```
# Click "Create new pull request" on GitHub repo, mark the base as the branch that will be merged into in "base". The branch name can be left as is or specify "@{xxdays}" or "@{YYYY-MM-DD}" which is the status of the base branch xx days ago or at YYYY-MM-DD
# In "compare", specifiy the branch or tag (by typing) that want to marge into base branch
# Some syntaxes can be used: HEAD^ (previous commit of HEAD), <branch>@{xxdays}, <branch>@{YYYY-MM-DD}...
```

## Config SSH key for multiple accounts (can only be saved in user default directory, i.e. User/\<user-name\>)

```
# Beware of the indentation
Host github.com-<custom-name-of-key>
 HostName github.com
 User git
 AddKeysToAgent yes
 IdentityFile ~/.ssh/<key-file-name>
```

## Generate SSH key for specific account

```
# Create .ssh folder in current tracked repo
  mkdir .ssh

# Add .ssh folder into .gitignore file-name, then trace to .ssh folder
  cd .ssh

# Generate key using following method
  ssh-keygen -t rsa -C "<email-address-dedicated-to-github-account>"

# Set key file name to be the same as in IdentityFile property in SSH config file

# Check and move the key from .ssh folder to user default folder if not located in that folder

# Set up remote using SSH method
  git remote add <remote-reference-name> git@github.com-<customer-name-in-config>:<user-name-or-organisation-name>/<git-file-name>.git
```

## Publish back to GitHub

```
# Set publish type
  git config --global push.default <simple/matching>
```

## Populate a folder into current tracked repo

```
# Use ~/<directory> if if is located in user default folder
# Use /* as following if all files and folders are to be populated
  cp -R <directory-of-folder>/*
```
