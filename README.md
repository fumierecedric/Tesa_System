# Tesa System

## Introduction

202511_Tesa_MA

## Readme

```sh
touch README.md
```

## Git

### Initialize Git repository

```sh
git init
```

### Add .gitignore

```sh
cat >> .gitignore << 'EOF'
# macOS Finder folder attributes
.DS_Store
EOF
```

### Setup main branch

```sh
git branch -M main
```

### Create a first commit

```sh
git add .
git commit -m "Initial commit"
```

### Create a GitHub repository

```sh
gh repo create Tesa_System --public --source=. --remote=origin --push
```


### Add remote repository

```sh
git remote add origin git@github.com:fumierecedric/Tesa_System.git
```

### Push to remote repository

- The `-u` flag sets the upstream branch for the current branch, allowing you to use `git push` without specifying the remote and branch name in the future.

```sh
git push -u origin main
```
