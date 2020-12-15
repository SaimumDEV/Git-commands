# git-commands

Essential about git commands and learning

# Git

Git command reference.

## Table of contents

- [Generating a new SSH key and linking to your machine](#Generating-a-new-SSH-key-and-linking-to-your-machine)
- [Push to a new Git repository](#Push-to-a-new-Git-repository)
- [Download all files from Git repository to a local directory](#Download-all-files-from-Git-repository-to-a-local-directory)
- [Initializing a repository in an existing directory](#initializing-a-repository-in-an-existing-directory)
- [Push an existing repositorys](#Push-an-existing-repository)
- [Pull update and push](#Pull-update-and-push)

## Generating a new SSH key and linking to your machine

first open git bash and Paste the text below, substituting in your GitHub email address.
`$ ssh-keygen -t ed25519 -C "your_email@example.com`

```bash
*Note:* If you are using a legacy system that does not support the Ed25519 algorithm, use:
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location. and hits enter until it finish.

now got to local

```bash
cd C:\Users\UserName\.ssh  *or saved location*
```

open id_rsa_pub/id_rsa and copy `ssh-rsa generated_code`
Now go to github account and click your profile photo, then click Settings.Click New SSH key or Add SSH key. Give any title and Paste your key into the "Key" field.Now sumit process.

## Push to a new Git repository

If you have a project on your computer and you just created an empty Git repository in GitHub, use these commands to upload everything to Git.

```bash
cd your-directory
git init
git remote add origin git@github.com:your-username/your-repo.git
git add .
git commit -m "Message"
git push -u origin master
```

```bash
cd your-directory
echo "# Repository" >> README.md
git init
git add README.md
git commit -m "Message"
git branch -M main
git remote add origin git@github.com:your-username/your-repo.git
git push -u origin main

```

## Download all files from Git repository to a local directory

The opposite of the above option - for example, if your repository exists in GitHub, and you're working on it in a different local computer. Run this command outside of where you want the new directory to appear (not within the directory you want it to appear).

```bash
git clone git@github.com:your-username/your-repo.git     # using SSH
git clone https://github.com/your-username/your-repo.git # using HTTPS
```

## Push an existing repository

```bash
git remote add origin git@github.com:your-username/your-repo.git
git branch -M main
git push -u origin main
```

## Pull update and push

When you want to first pull updated work and push to remote.

```bash
git status
git stash/git stash save/git stash -u
git pull --rebase
git stash pop
```

```bash
git status
git add .
git commit -m "message"
git push
```

## Force a push or pull

When you really want your local repository to override the remote.

```bash
git push -f origin master
git pull -f origin master
```

## Merging changes from remote pull request with conflicts

Make a new branch with their changes.

```bash
git checkout -b their-branch master
git pull their.git master
```

Play with the files and commit them.

```bash
git add files
git commit -m “Message"
git push origin master
```

Merge back into your branch.

```bash
git checkout master
git merge --no-ff <their-branch) (:wq!)
git push origin master
```

## Remove branch

Put a `:` in front to remove instead of update remotely.

```bash
git push origin :branch-name
```

Use `--delete` or `-D` for local.

```
git branch --delete branch-name
```

## Replace master with contents of another branch

```bash
git checkout branch-name
git merge -s ours master
git checkout master
git merge branch-name
```

## Remove all local branches except master

```bash
git branch | grep -v "master" | xargs git branch -D
```

More than one branch may be added to the grep. To remove all local branches except "master" and "develop":

```bash
git branch | grep -v "master\|develop" | xargs git branch -D
```

## Allow empty commit

Fix the problem of git hooks claiming everything is "Up-to-date".

```bash
git push production master
git commit --allow-empty -m 'push to execute post-receive'
git push production master
```

## Merge new-feature branch into master

Merge branches.

```bash
git checkout master
git pull origin master
git merge new-feature
git push origin master
```

## Switch to branch that exists on origin

```bash
git fetch --prune --all
git checkout other-branch
```

## Fetch branch from origin

```bash
git fetch origin
git checkout --track origin/<remote_branch_name>
```

## Accept all incoming changes

```bash
git pull -Xtheirs
```

## Rebase from develop

```bash
git fetch --prune --all
git rebase origin/develop
git pull
git push
```

## Stashing

Put your changes away and switch to another branch

```bash
git stash
git checkout -b new-branch
git stash pop
```

## Accidentally committed to develop and want to move that commit to a branch

```bash
git branch new-branch
git reset HEAD~1
git checkout <files>
```

## Remove one file from Git cache

Remove one cached file.

```bash
git rm -r —-cached file.txt
```

## Override entire local directory

If you have some merge conflicts, or accidentally started to make a change to your local directory before pulling the changes from the master, here's how you can revert your local directory to what's on GitHub.

```bash
git fetch --all
git reset --hard origin/master
```

## Ignore a directory

If you've been tracking a directory and later decide to ignore the whole directory, simply adding it to `.gitignore` isn't enough. First you must add the directory to .gitignore, then run this command:

```bash
git rm -r --cached your-directory
```

Then push the changes.

## Add .gitignore to an existing repository

Similar to above, but if you've added a `.gitignore` with a lot of changes.

```bash
git rm -r --cached .
git add .
git commit -m "Message"
```
