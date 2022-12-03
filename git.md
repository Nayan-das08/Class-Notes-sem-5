# learning Version Control using Git
![[Pasted image 20221203213144.png]]


## level 1 - basic shit

| from      | to        | command                        | remarks                                |
| --------- | --------- | ------------------------------ | -------------------------------------- |
| untracked | staged    | `git add <file>`           | file will be staged                    |
| staged    | committed | `git commit -m "some message"` | the files in staged area are committed |
| staged    | modified  | modify the file                | the file will be given modified tag    |
| modified  | staged    | `git add <file>`           | the changes will be staged             |
| staged    | committed | `git commit -m "some message"` | the files in staged area are committed |

## level 2 - undoing things

### un-modifying a modified file
discard changes in working directory
- `git restore <file>`
- `git checkout -f`
	- this is a separate command, discussed later
	- also, dangerous

### un-staging changes
suppose you made some changes to a staged (or committed) file and staged it using `git add <file>`.

to un-stage the changes, you can use 
- `git restore --staged <file>`
- `git reset <file>`
	- this one is dangerous, so avoid 

once un-staged, the file will be in **modified** mode again

---
# `git reset` and `git checkout`
git maintains three *trees*, or collection of files
if all are same, `git status` will give "nothing to commit, working tree clean"

1. <u>HEAD</u>
	- `bb312f6 (HEAD -> master) three`
	- `HEAD` represents the *current commit* where the repo is pointing to
	- this currently is at the tip of the branch
2. <u>index</u>
	- it is the *proposed next commit*
	- staging area to be honest
	- if this is different from HEAD, `git status` will give "Changes to be committed" message
3. <u>working tree</u>
	- where we *actually work*
	- if this is different from index and working directory, `git status` will give "Changes not staged for commit" message

![[Pasted image 20221204004005.png]]

## `git reset`
`git reset` can manipulate these three tree

### Move `HEAD`
- `git reset --soft ...` moves the HEAD leaving the index and working tree as it is
- this results in moving the HEAD to some previous commit
- but *`git status`* gives "*Changes to be committed*"
- the changes that made the skipped commit are left *staged*
- we can now *re-commit* the changes using `git commit` again
- `git reset --soft HEAD~` moves the HEAD *one commit back*
- `git reset --soft HEAD~n` moves the HEAD *n commit back*
- `git reset --soft <commit>` moves the HEAD to the given commit
	- the changes made between the last commit (from which we reset) and the one where we landed are now in staged area
	- all those changes are now shown in green, i.e. *modified*

### updating index
- *`git reset --mixed ...`* or simply *`git reset ...`* will move the HEAD and well as the index, leaving working tree untouched
- *`git status`* gives "*Changes not staged for commit*"
- the changes made in the skipped commits are *un-staged*
	- the changes have to be added before commit
	- we can use `git add <file>` or `git commit -a`
- we can now *re-do the changes* that we mistakenly *committed* and the do `git commit` again

### updating working tree
- *`git reset --hard`* will move the HEAD, index and the working tree
- *`git status`* will give "*nothing to commit, working tree clean*"
- all the changes made in the skipped commits are overwritten in the working directory

---

# commit log of remote repo
- `git fetch`
- `git log origin/master`
- you can also do `git diff origin/master` as well

