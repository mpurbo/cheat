# Starting Up

### Create local git, initial push to remote
```bash
git init
git add .
git commit -a -m "Initial project creation"
git remote add origin [username@url:project.git]
git push origin master
```

### Setting remote URL (github)
```bash
git remote set-url origin [username@url:project.git]
```

### Check remote origin
```bash
git remote show origin
```

### Replace local repo with remote (rewrite all local changes)
```bash
git fetch --all
git reset --hard origin/master
```



