# Demo Project README

## General commans

```
# Initiate new git project
git init

# Add all files into tracked project
git add .

# Commit all changes
git commit

# Set up remote
git remote add <remote-name> <repo-address>

# Clone a repo into local machine
git clone origin <repo-address> <optional: folder-name-if-needed>

# Stage changes
git add <.-if-add-all-changes>

# Publish changes
git push <optional: remote-name> <optional: branch-name>

# Fetch changes
git fetch <optional: remote-name> <optional: branch-name>

# Get new changes
git pull <optional: remote-name> <optional: branch-name>
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