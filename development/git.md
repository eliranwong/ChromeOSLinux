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

Trouble-shooting git push large files: https://stackoverflow.com/questions/15843937/git-push-hangs-after-total-line

solution:

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
