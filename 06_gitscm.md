# Rebase
Rebasing replays changes from one line of work onto another in the order they were introduced, whereas merging takes the endpoints and merges them together.
![](src/basic-rebase-1.png)
```bash
[abc@abc]$ git checkout experiment
[abc@abc]$ git rebase master

First, rewinding head to replay your work on top of it...
Applying: added staged command
```
This operation works by going to the common ancestor of the two branches (the one you’re on and the one you’re rebasing onto), getting the diff introduced by each commit of the branch you’re on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.
![](src/basic-rebase-3.png)
```bash
[abc@abc]$ git checkout master
[abc@abc]$ git merge experiment
# Fast Forward
```
![](src/basic-rebase-4.png)
## Example
![](src/interesting-rebase-1.png)
```bash
[abc@abc]$ git rebase --onto master server client
```
![](src/interesting-rebase-2.png)
```bash
[abc@abc]$ git checkout master
[abc@abc]$ git merge client
```
![](src/interesting-rebase-3.png)
```bash
[abc@abc]$ git rebase master server
```
![](src/interesting-rebase-4.png)
```bash
[abc@abc]$ git checkout master
[abc@abc]$ git merge server

[abc@abc]$ git branch -d client
[abc@abc]$ git branch -d server
```
![](src/interesting-rebase-5.png)

# The Perils of Rebasing
TODO