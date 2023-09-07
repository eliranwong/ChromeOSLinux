# git

https://guides.github.com/

https://guides.github.com/introduction/git-handbook/

# Global Configuration

> git config --global user.name myusername

> git config --global user.email myusername@email.com

# User Configurations

Edit file ~/.gitconfig

> nano ~/.gitconfig

* [user]<br>
* username = myusername<br>
* email = myusername@email.com

# Common Commands

e.g.

> git add README.md

> git commit -m "update file(s)"

> git push

or

> git push --set-upstream origin main

or

> git push -u origin main

or

> git push --set-upstream origin main

To manage branches:

To create:

> git checkout -b new_branch

To switch to a remote branch:

> git branch -r

> git checkout branch_name

To delete:

> git branch -D branch_name

To list all non-staged files:

> git ls-files --other --modified --exclude-standard

To overwrite changes in local files:

> git fetch --all

> git reset

Trouble-shoot hanging for pushing large files:

> git config --global http.postBuffer 157286400

read more about this solution at https://stackoverflow.com/questions/15843937/git-push-hangs-after-total-line

# Discard Local Changes

There are different ways to discard local changes and pull the latest changes from the GitHub repository, depending on your situation and preference. Here are some common methods:

- If you want to discard all local changes and commits that are not pushed to the remote repository, you can use `git reset --hard` followed by `git pull`. This will reset your local repository to the same state as the remote repository and then pull the latest changes. For example¹²:

```bash
git reset --hard
git pull
```

- If you want to discard only local changes that are not committed, but keep your local commits that are not pushed to the remote repository, you can use `git checkout .` followed by `git pull`. This will revert all modified files to their original state and then pull the latest changes. For example²:

```bash
git checkout .
git pull
```

- If you want to temporarily save your local changes and apply them later, after pulling the latest changes from the remote repository, you can use `git stash` followed by `git pull` and `git stash pop`. This will store your local changes in a stash, update your local repository with the remote changes, and then reapply your stashed changes. For example²:

```bash
git stash
git pull
git stash pop
```
