# Git branching
## Blob
```bash
[abc@abc]$ git init
# |   ├── objects
# |   │   ├── info
# |   │   └── pack
[abc@abc]$ vim README && vim test.rb && vim LICENSE
[abc@abc]$ git add README test.rb LICENSE
# │   ├── objects
# │   │   ├── 1f
# │   │   │   └── d7e72fa9a80fb4c5a0a3727f354e2f28f06ae4
# │   │   ├── 3f
# │   │   │   └── 31c62769df3e457badfc980eb82d20074a891d
# │   │   ├── d8
# │   │   │   └── e3ed767017dac0d1d27582fe46a68591e2fdb5
# │   │   ├── info
# │   │   └── pack
# │   └── refs
# │       ├── heads
# │       └── tags
# ├── LICENSE
# ├── README
# └── test.rb
[abc@abc]$ git commit -m 'initial commit'
# │   ├── objects
# │   │   ├── 1f
# │   │   │   └── d7e72fa9a80fb4c5a0a3727f354e2f28f06ae4
# │   │   ├── 3f
# │   │   │   └── 31c62769df3e457badfc980eb82d20074a891d
# │   │   ├── 47
# │   │   │   └── 5c10ded3127cb6e11c5c5f7c9b297bf48f7a3c
# │   │   ├── 9e
# │   │   │   └── 13aaf8ab2aecd135535639111b63da462d4427
# │   │   ├── d8
# │   │   │   └── e3ed767017dac0d1d27582fe46a68591e2fdb5
# │   │   ├── info
# │   │   └── pack
# │   └── refs
# │       ├── heads
# │       │   └── master
# │       └── tags
```
![](src/branch1.png)
3 files -> 3 blobs  
Directory Structure(tree) -> 1 blob  
Meta data(commit message and ...) -> 1 blob  
# Examples
![](src/branch2.png)
![](src/branch3.png)
![](src/branch4.png)

# Merge Example 1
![](src/branch5.png)
```bash
[abc@abc]$ git checkout master
[abc@abc]$ git merge hotfix

Updating f42c576..3a0874c
Fast-forward
 index.html | 2 ++
 1 file changed, 2 insertions(+)
```
![](src/branch6.png)

# Merge Example 2(without conflict)
![](src/branch7.png)
```bash
[abc@abc]$ git checkout master
Switched to branch 'master'
[abc@abc]$ git merge iss53
Merge made by the 'recursive' strategy.
index.html |    1 +
1 file changed, 1 insertion(+)
```
![](src/branch8.png)  
```bash
# Conflict -> no new commit
# Try
[abc@abc]$ git status
[abc@abc]$ git mergetool
```
# command
```bash
[abc@abc]$ git branch
[abc@abc]$ git branch -v
[abc@abc]$ git branch --merged
[abc@abc]$ git branch --no-merged
[abc@abc]$ git branch --all
[abc@abc]$ git branch testing
[abc@abc]$ git checkout testing
[abc@abc]$ git branch -d hotfix  # delete branch

[abc@abc]$ git branch --move bad-branch-name corrected-branch-name  # local change
[abc@abc]$ git push --set-upstream origin corrected-branch-name  #  To let others see the corrected branch on the remote
[abc@abc]$ git branch --all

* corrected-branch-name
  main
  remotes/origin/bad-branch-name
  remotes/origin/corrected-branch-name
  remotes/origin/main

# Notice that you’re on the branch corrected-branch-name and it’s available on the remote. However, the branch with the bad name is also still present there but you can delete it by executing the following command:
[abc@abc]$ git push origin --delete bad-branch-name
```
