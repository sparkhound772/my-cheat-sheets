### Authenticate

`ps aux | ssh-agent`

`eval $(ssh-agent)`

`ssh-add ~/.ssh/githubkey.pub`

`ssh -T git@github.com`

Or without caching the key:

`ssh -i ~/.ssh/githubkey.pub -T git@github.com`

### Logs

Log (simple):

`git --no-pager log --oneline`

Log (graph):

`git log --branch`

### Diff

Diff between WD and staging area (index):

`git diff`

Diff between last commit and staging area:

`git diff --staged`

or:

`git diff --cached`

Diff between two commits:

`git diff <commit-hash-1> <commit-hash-2>`

Diff within file:

`git diff <file>`

### Configuration

Set username within repo:

`git config user.name <myname>`

Set user e-mail within repo:

`git config user.email <my-e-mail>`

Change initial branch name globally:

`git config --global init.defaultBranch <name>`

Set the default editor to be used with Git globally:

`git config --global core.editor "vim"`

### Remote, fetch and pull

Show remote:

`git remote show origin`

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

`git fetch origin` 

Pull changes from remote (fetch + merge):

`git pull origin BRANCHNAME`

Set new remote url after repository name has been changed:

`git remote set-url origin URL`

Clone repository:

`git clone <url>`

### Staging and tracking

Stage changes and track new files:

`git add <file>`

Unstage specific file (and untrack new tracked file):

`git rm --cached <file>`

Unstage all files (and untrack new tracked files):

`git reset HEAD`

### Committing

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

### More resetting and reverting

Undo uncommitted (but staged) changes in files (and remove new files):

`git reset --hard HEAD`

Undo uncommitted (and unstaged) changes in files (but won't remove new and untracked files for some reason):

`git reset --hard HEAD`

Same as previous one but for specific files it seems:

`git restore FILE`

Remove uncommitted (and untracked) new files (but don't remove changes in existing files for some reason):

`git clean -df`

Revert already pushed commit:

`git revert -m "message" HEAD`

### Branches

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
