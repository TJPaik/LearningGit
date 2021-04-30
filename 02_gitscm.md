# Git life cycle
![](src/lifecycle.png "lifecycle")
# .gitignore
TODO : will be added
# Undoing Things
## modify last commit
```bash
[abc@abc]$ git commit --amend
# change commit message
# or 
[abc@abc]$ git commit -m 'initial commit'
[abc@abc]$ git add forgotten_file
[abc@abc]$ git commit --amend
```
## Unstaging a staged File
```
[abc@abc]$ git add README.md
[abc@abc]$ git mv A.md B.md
[abc@abc]$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    A.md -> B.md
        new file:   README.md

[abc@abc]$ git reset HEAD README.md
[abc@abc]$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        renamed:    A.md -> B.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

```
# Unmodifying
```
[abc@abc]$ git status

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   CONTRIBUTING.md

[abc@abc]$ git checkout -- CONTRIBUTING.md
[abc@abc]$ git status

On branch master
nothing to commit, working tree clean
```
# Restore
Git version 2.23.0 introduced a new command: `git restore`. It’s basically an alternative to git reset which we just covered. From Git version 2.23.0 onwards, Git will use `git restore` instead of `git reset` for many undo operations.

```bash
[abc@abc]$ git add *
[abc@abc]$ git status

On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   CONTRIBUTING.md
	renamed:    README.md -> README

# Right below the “Changes to be committed” text, it says use git restore --staged <file>…​ to unstage. So, let’s use that advice to unstage the CONTRIBUTING.md file:

[abc@abc]$ git restore --staged CONTRIBUTING.md
[abc@abc]$ git status

On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    README.md -> README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   CONTRIBUTING.md
```

```bash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   CONTRIBUTING.md

# It tells you pretty explicitly how to discard the changes you’ve made. Let’s do what it says:

[abc@abc]$ git restore CONTRIBUTING.md
[abc@abc]$ git status

On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    README.md -> README
```

# Remote Repository
```bash
[abc@abc]$ git clone https://github.com/schacon/ticgit

Cloning into 'ticgit'...
remote: Reusing existing pack: 1857, done.
remote: Total 1857 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (1857/1857), 374.35 KiB | 268.00 KiB/s, done.
Resolving deltas: 100% (772/772), done.
Checking connectivity... done.

[abc@abc]$ cd ticgit
[abc@abc]$ git remote

origin
# 'origin' remote repo(default)

[abc@abc]$ git remote -v 

origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```
## Adding Remote Repositories

```bash
[abc@abc]$ git remote

origin

# git remote add <alias, shortname> <url>
[abc@abc]$ git remote add pb https://github.com/paulboone/ticgit
[abc@abc]$ git remote -v

origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
pb	https://github.com/paulboone/ticgit (fetch)
pb	https://github.com/paulboone/ticgit (push)

[abc@abc]$ git fetch pb

remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paulboone/ticgit
 * [new branch]      master     -> pb/master
 * [new branch]      ticgit     -> pb/ticgit

# $ git fetch <remote>
# fetch all data in remote repo.
```
If you clone a repository, the command automatically adds that remote repository under the name `origin`.

It’s important to note that the `git fetch` command only downloads the data to your local repository — it doesn’t automatically merge it with any of your work or modify what you’re currently working on. You have to merge it manually into your work when you’re ready.

If your current branch is set up to track a remote branch, you can use the `git pull` command to automatically fetch and then merge that remote branch into your current branch. 

The `git clone` command automatically sets up your local master branch to track the remote master branch (or whatever the default branch is called) on the server you cloned from. Running `git pull` generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.

```bash
# git push <remote> <branch>
[abc@abc]$ git push origin master
```
## Rename & Remove remote repo 
```bash
[abc@abc]$ git remote rename pb paul
[abc@abc]$ git remote

origin
paul

[abc@abc]$ git remote rmove paul
[abc@abc]$ git remote

origin
```

