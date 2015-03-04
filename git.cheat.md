# Git Cheat Sheet

A collection of git-related tasks and commands that I frequently used for my daily tasks.

## Project Management

### Starting

When starting a project locally, after creating some initial files and creating a remote repo somewhere, I always do following steps to setup a repo:
```bash
git init
git add .
git commit -a -m "Initial project creation"
git remote add origin [username@url:project.git]
git push origin master
```
`[username@url:project.git]` should be replaced with remote repo specification, e.g.
```
git@gitlab.com:username/project.git
https://username@bitbucket.org/username/project.git
https://github.com/username/project.git
```

### Basic Commands
