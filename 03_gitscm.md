# Tagging
## Tag
For each commit...
* Examples:
    * v0.1
    * v1.3
    * v1.8.5
    * ...
```bash
[abc@abc]$ git tag
v0.1
v1.3
...
[abc@abc]$ git tag -l "v1.8.5*"
v1.8.5
v1.8.5-rc0
```
## Show Tag
```bash
[abc@abc]$ git show v1.8.5

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
```
## Annotated Tag
```bash
[abc@abc]$ git tag -a v1.4 -m "My version 1.4"
[abc@abc]$ git tag
v1.8.5
v1.8.5-rc0
v1.4
```
## Lightweight Tag
```bash
[abc@abc]$ git tag v1.4-lw
[abc@abc]$ git tag
v1.8.5
v1.8.5-rc0
v1.4
v1.4-lw
```
## Tagging Later
```bash
[abc@abc]$ git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
166ae0c4d3f420721acbb115cc33848dfcc2121a Create write support
9fceb02d0ae598e95dc970b74767f19372d61af8 Update rakefile
964f16d36dfccde844893cac5b347e7b3d44abbc Commit the todo
8a5cbc430f1a9c3d00faaeffd07798508422908a Update readme

[abc@abc]$ git tag -a v1.2 9fceb02
```

## Send Tag to Remote
`git push` isn't enough.
```bash
[abc@abc]$ git push origin v1.5

Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5

# If you have a lot of tags that you want to push up at once, you can also use the --tags option to the git push command. This will transfer all of your tags to the remote server that are not already there.

[abc@abc]$ git push origin --tags

Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw
```
# Deleting Tag
```bash
[abc@abc]$ git tag -d v1.4-lw

Deleted tag 'v1.4-lw' (was e7d5add)
```
Note that this does not remove the tag from any remote servers. There are two common variations for deleting a tag from a remote server.

The first variation is `git push <remote> :refs/tags/<tagname>:`
```bash
[abc@abc]$ git push origin :refs/tags/v1.4-lw
To /git@github.com:schacon/simplegit.git
 - [deleted]         v1.4-lw
```
The way to interpret the above is to read it as the null value before the colon is being pushed to the remote tag name, effectively deleting it.

The second (and more intuitive) way to delete a remote tag is with:

```bash
[abc@abc]$ git push origin --delete <tagname>
```
## Tag can be used to checkout
If you want to view the versions of files a tag is pointing to, you can do a git checkout of that tag, although this puts your repository in “detached HEAD” state, which has some ill side effects.