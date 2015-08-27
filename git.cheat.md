# Git Cheat Sheet

A collection of git-related tasks and commands that I occasionally used for my daily tasks but am too lazy to remember.

## Project Management

### Setting up

When starting a project locally, after creating some initial files and creating a remote repo somewhere, I always do following steps to setup a repo:
```bash
git init
git add .
git commit -a -m "Initial project creation"
git remote add origin $REMOTE_REPO
git push origin master
```
`$REMOTE_REPO` should be the remote repo specification, e.g.
```
git@gitlab.com:username/project.git
https://username@bitbucket.org/username/project.git
https://github.com/username/project.git
```

To check current origin:
```
git remote show origin
```

### Cloning specific revision

To clone a specific version `$REVISION_ID`:
```bash
# make a new blank repository in the current directory
git init

# add a remote
git remote add origin $REMOTE_REPO

# fetch and checkout revision
git fetch origin
git checkout $REVISION_ID
```

### Moving repository

Here's the steps to copy/move a project from one repository to another:
```bash
mkdir $TEMP_REPO_FOLDERNAME                       # create a new folder
cd $TEMP_REPO_FOLDERNAME
git init --bare .git                              # create a bare repo
git remote add origin $SOURCE_REMOTE_URL          # add a remote
git fetch origin refs/heads/*:refs/heads/*        # fetch heads
git fetch origin refs/tags/*:refs/tags/*          # fetch tags
git init                                          # reinit work tree
git checkout master                               # checkout a branch
git remote rm origin                              # remove remote repo
git remote add origin $TARGET_REMOTE_URL          # new remote url
git push -u origin master                         # now push master
git push --all                                    # now push all other branches
```

## Syncing

### Syncing a fork

```bash
git fetch upstream
git checkout master
git merge upstream/master
```
Source: [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)

### Rebase

Rebase is essentially: pull down the remote changes, rewind your local branch, then replays all your changes over the top of your current branch one by one, until you’re all up to date.
```bash
git pull –rebase
```

Source: [THE DIFFERENCE BETWEEN GIT PULL, GIT FETCH AND GIT CLONE (AND GIT REBASE)](http://blog.mikepearce.net/2010/05/18/the-difference-between-git-pull-git-fetch-and-git-clone-and-git-rebase/)

## Undo, replace, remove

<table>
    <tr><th>Purpose</th><th>Command</th></tr>
    <tr>
        <td>Undo file update.</td>
        <td><code>git checkout -- [file]</code></td>
    </tr>
    <tr>
        <td>Undo uncommitted (but staged) removed file.</td>
        <td><code>git checkout [commit-sha-where-the-file-existed] [file]</code></td>
    </tr>
    <tr>
        <td>Undo commit and discard changes.</td>
        <td>
            <pre>
## 1 commit
git reset --hard HEAD~1 
## 5 commit
git reset --hard HEAD~5
## specific commit
git reset --hard [commit-sha]
            </pre>
        </td>
    </tr>
    <tr>
        <td>Undo last commit but keep the changes.</td>
        <td><code>git reset HEAD~1</code></td>
    </tr>
    <tr>
        <td>Undo last commit but keep the changes and index.</td>
        <td><code>git reset --soft HEAD~1</code></td>
    </tr>
    <tr>
        <td>Change latest commit comment.</td>
        <td><code>git commit --amend -m "New commit message"</code></td>
    </tr>
    <tr>
        <td>Undelete/restore file (get file from a specific commit).</td>
        <td><code>git checkout [commit-sha] [filename]</code></td>
    </tr>
    <tr>
        <td>Bulk undo: remove staged and working directory changes.</td>
        <td><code>git reset --hard</code></td>
    </tr>
    <tr>
        <td>Bulk undo: remove untracked files.</td>
        <td><code>git clean -f -d</code></td>
    </tr>
    <tr>
        <td>Bulk undo: remove untracked files including ignored files (e.g. build products).</td>
        <td><code>git clean -f -x -d</code></td>
    </tr>
    <tr>
        <td>Replace local rep with remote (rewrite all local changes)</td>
        <td>
            <pre>
git fetch --all
git reset --hard origin/master
            </pre>
        </td>
    </tr>
    <tr>
        <td>Remove a file from the repository without deleting it from the local filesystem (useful if we add some files to .gitignore and we want to untrack it).</td>
        <td>
            <pre>
# 1 file:
git rm --cached [file] 

# multiple files
git rm -r --cached .
git add .  
            </pre>
        </td>
    </tr>
    <tr>
        <td>Delete the last commit already pushed to remote (e.g. origin last commit was [hash])</td>
        <td><code>git push origin +[hash]^:master</code></td>
    </tr>
</table>

## Branch

<table>
    <tr><th>Purpose</th><th>Command</th></tr>
    <tr>
        <td>Create branch.</td>
        <td><code>git branch [branch-name]</code></td>
    </tr>
    <tr>
        <td>Create branch from specific commit.</td>
        <td><code>git branch [branch-name] [sha1-of-commit]</code></td>
    </tr>
    <tr>
        <td>Create branch from unstaged/uncommitted changes on master.</td>
        <td>
            <pre>
git checkout -b new_branch
git commit -am "edited"
git checkout master
git status
            </pre>
        </td>
    </tr>
    <tr>
        <td>Switch branch.</td>
        <td><code>git checkout [branch-name]</code></td>
    </tr>
    <tr>
        <td>Create branch and switch.</td>
        <td><code>git checkout -b [branch-name]</code></td>
    </tr>
    <tr>
        <td>Push branch that has the same name as remote tag</br>Source: <a href="http://stackoverflow.com/questions/9378760/git-push-local-branch-with-same-name-as-remote-tag">git push local branch with same name as remote tag</a></td>
        <td><code>git push origin refs/heads/[name]:refs/heads/[name]</code></td>
    </tr>
    <tr>
        <td>Pull other branch.</td>
        <td><code>git pull origin [branch-name]</code></td>
    </tr>
    <tr>
        <td>Merge branch.</td>
        <td><code>git merge [branch-name]</code></td>
    </tr>
    <tr>
        <td>Push branch to remote origin.</td>
        <td><code>git push origin [branch-name]</code></td>
    </tr>
    <tr>
        <td>Delete branch locally.</td>
        <td><code>git branch -d [branch-name]</code></td>
    </tr>
    <tr>
        <td>Force delete branch locally (unmerged branch).</td>
        <td><code>git branch -D [branch-name]</code></td>
    </tr>
    <tr>
        <td>Delete remote branch.</td>
        <td>
            <pre>
# git >= v1.5
git push origin :[branch-name]

# git >= v1.7
git push origin --delete [branch-name]
            </pre>
        </td>
    </tr>
    <tr>
        <td>Compare branches (find which file has been modified).</td>
        <td><code>git diff --name-status [branch-name-1]..[branch-name-2]</code></td>
    </tr>
    <tr>
        <td>Compare files in branches.</td>
        <td><code>git diff [branch-name-1] [branch-name-2] — filepath</code></td>
    </tr>
    
</table>

## Tag

<table>
    <tr><th>Purpose</th><th>Command</th></tr>
    <tr>
        <td>Create tag.</td>
        <td><code>git tag -a [tagname] -m "comment"</code></td>
    </tr>
    <tr>
        <td>Push tag to remote origin.</td>
        <td><code>git push origin [tagname]</code></td>
    </tr>
    <tr>
        <td>Delete tag locally.</td>
        <td><code>git tag -d [tagname]</code></td>
    </tr>
    <tr>
        <td>Delete remote tag.</td>
        <td><code>git push origin :refs/tags/[tagname]</code></td>
    </tr>
</table>

## Subtree

A sample procedure on how to create a subtree:
```bash
# add remote pointing to other repo
git remote add test-subtree https://github.com/mpurbo/test-subtree.git
# add subtree from other repo
git subtree add --prefix=test-subtree/ test-subtree master --squash
# push update to parent so it has subtree's files
git push origin master

# make changes in the subtree ...

# push update to parent first
git push origin master
# push subtree
git subtree push --prefix=test-subtree test-subtree private-push-branch
```

## Configuration

### Increasing upload size limit

When pushing file causes the following error:
```
error: RPC failed; result=55, HTTP code = 0
fatal: The remote end hung up unexpectedly
```
Most likely this is because the file uploaded exceeded current size limit. To increase the limit, use `http.postBuffer` setting. Following example increase the size limit to 500MB:
```bash
git config --global http.postBuffer 524288000
```

### Formatting log output

To make `git log` output much less boring and easier on the eye use: 
```bash
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
This will create an alias `lg` that produces pretty output. Use `-p` to display updated lines:
```bash
git lg
git lg -p
```
Source: [A better git log](https://coderwall.com/p/euwpig)

### Colorize output

To enable color for git commands:
```bash
git config --global color.ui true
```
Source: [Colors in Git](http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#Colors-in-Git)

## Links

- [Official Git Reference](http://git-scm.com/docs)
- [Git Reference](http://gitref.org/index.html)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials/)
- [Gitチートシート](http://qiita.com/ktaro/items/1d8c8ae698a88b1d6f0f)
- [Github's cheatsheet](https://help.github.com/articles/git-cheatsheet/)
- [Git tips from the trenches](https://ochronus.com/git-tips-from-the-trenches/)
- [Git Howto: Revert a Commit Already Pushed to a Remote Repository](http://christoph.ruegg.name/blog/git-howto-revert-a-commit-already-pushed-to-a-remote-reposit.html)
- [How to undo (almost) anything with Git](https://github.com/blog/2019-how-to-undo-almost-anything-with-git)
- [Git pretty](http://justinhileman.info/article/git-pretty/)
