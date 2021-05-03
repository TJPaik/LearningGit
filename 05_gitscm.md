# hmm
```bash
git ls-remote <remote>
git remote show <remote>
```
# git fetch origin
![](src/remote-branches-3.png)  
# Adding another server as a remote
![](src/remote-branches-4.png)  
not changed yet...  
## git fetch teamone
![](src/remote-branches-5.png)  

# Pushing
You can use private branches for work you don’t want to share, and push up only the topic branches you want to collaborate on.

If you have a branch named `serverfix` that you want to work on with others, you can push it up the same way you pushed your first branch. Run `git push <remote> <branch>`:

```bash
[abc@abc]$ git push origin serverfix

Counting objects: 24, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done.
Total 24 (delta 2), reused 0 (delta 0)
To https://github.com/schacon/simplegit
 * [new branch]      serverfix -> serverfix
```

This is a bit of a shortcut. Git automatically expands the serverfix branchname out to `refs/heads/serverfix:refs/heads/serverfix`, which means, “Take my serverfix local branch and push it to update the remote’s serverfix branch.” 
We’ll go over the `refs/heads/` part in detail in `Git Internals`, but you can generally leave it off.
You can also do `git push origin serverfix:serverfix`, which does the same thing — it says, “Take my serverfix and make it the remote’s serverfix.” You can use this format to push a local branch into a remote branch that is named differently. 
If you didn’t want it to be called serverfix on the remote, you could instead run git push origin serverfix:awesomebranch to push your local serverfix branch to the awesomebranch branch on the remote project.

The next time one of your collaborators fetches from the server, they will get a reference to where the server’s version of serverfix is under the remote branch `origin/serverfix`:

```bash
[abc@abc]$ git fetch origin
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/schacon/simplegit
 * [new branch]      serverfix    -> origin/serverfix
```
It’s important to note that when you do a fetch that brings down new remote-tracking branches, you don’t automatically have local, editable copies of them. In other words, in this case, you don’t have a new `serverfix` branch — you have only an `origin/serverfix` pointer that you can’t modify.

To merge this work into your current working branch, you can run git merge `origin/serverfix`. If you want your own `serverfix` branch that you can work on, you can base it off your remote-tracking branch:
```bash
[abc@abc]$ git checkout -b serverfix origin/serverfix

Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```
This gives you a local branch that you can work on that starts where `origin/serverfix` is.

# Tracking Branches
TODO
# Pulling
TODO
# Deleting Remote Branches
TODO
