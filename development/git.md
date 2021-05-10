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
