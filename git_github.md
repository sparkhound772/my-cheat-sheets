# SSH

Authenticate:

`ssh -i <KEY> -T git@github.com`

Change initial branch name globally:

`git config --global init.defaultBranch <name>`

Stage:

`git add <file>`

Unstage:

`git rm --cached <file>`

Commit:

`git commit -m "message"`

Create new branch and checkout to it:

`git checkout -b "branchname"`

Checkout to any branch:

`git checkout "branchname"`

Show branches:

`git branch`

Take work from branch2 and merge into branch1:

```
git checkout branch1
git merge branch2
```

Change current branch name:

`git branch -m <name>`

Add remote:

`git remote add origin <remote repo link>`

Push to remote:

`git chekout "branch to push"`
`git push -u origin main`

See remote:

`git remote`

Get changes from remote:

`git pull`

Clone repository:

`git clone <url>`
