## Quick setup - if you've done this kind of thing before
## or HTTPS/SSH https://~ / git@github.com:~
 Get started by creating a new file or uploading an existing file. We recommend every repository include a README, LICENSE, and .gitignore. 

## …or create a new repository on the command line
### what I chose
```bash
echo "# LearningGit" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/TJPaik/LearningGit.git (HTTPS)
git remote add origin git@github.com:TJPaik/LearningGit.git (SSH)
git push -u origin main
```

## …or push an existing repository from the command line
```bash
git remote add origin https://github.com/TJPaik/LearningGit.git (HTTPS)
git remote add origin git@github.com:TJPaik/LearningGit.git (SSH)
git branch -M main
git push -u origin main
```

## …or import code from another repository
```bash
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.  
Button `Import code`
```
