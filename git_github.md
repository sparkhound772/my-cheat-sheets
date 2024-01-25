Authenticate:

`ps aux | ssh-agent`

`eval $(ssh-agent)`

`ssh-add ~/.ssh/githubkey.pub`

`ssh -T git@github.com`

Or without cacheing the key:

`ssh -i ~/.ssh/githubkey.pub -T git@github.com`

Change initial branch name globally:

`git config --global init.defaultBranch <name>`

Show remote:

`git remote show origin`

Stage changes and track new files:

`git add <file>`

Unstage specific file (and untrack new tracked file):

`git rm --cached <file>`

Unstage all files (and untrack new tracked files):

`git reset HEAD`

Commit:

`git commit -m "message"`

Change the message for the last commit:

`git commit --amend -m "New message"`

Uncommit and discard changes to get back to state of last commit (also deletes new files)

`git reset --hard HEAD^`

Uncommit and unstage (and untrack new created tracked files) but keep changes:

`git reset HEAD^`

Uncommit, don't unstage or untrack and keep changes:

`git reset --soft HEAD^`

Undo uncommitted (but staged) changes in files (and remove new files):

`git reset --hard HEAD`

Undo uncommitted (and unstaged) changes in files (but won't remove new and untracked files for some reason):

`git reset --hard HEAD`

Same as previous one but for specific files it seems:

`git restore FILE`

Remove uncommitted (and untracked) new files (but don't remove changes in existing files for some reason):

`git clean -df`

Create new branch and checkout to it:

`git checkout -b "branchname"`

Checkout to any branch:

`git checkout "branchname"`

Show branches:

`git --no-pager branch -vv`

Take work from branch2 and merge into branch1:

```
git checkout branch1
git merge branch2
```

Change current branch name:

`git branch -m <name>`

Add remote:

`git remote add origin <remote repo link>`

OR

Set remote tracking when pushing:

`git checkout "branch to push"`
`git push -u origin main`

Pushes after remote has been set to track with `add` or `-u`:

`git push origin main`

See remote:

`git remote`

Fetch changes from remote:

`git fetch origin main` (i.e. `REMOTENAME BRANCHNAME`)

Pull changes from remote (fetch + merge):

`git pull origin main` (i.e. `REMOTENAME BRANCHNAME`)

Clone repository:

`git clone <url>`
