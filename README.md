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

## Environment Setup

### Create yml file for Conda environment

```sh
cat >> environment.yml << 'EOF'
name: tesa
channels:
- conda-forge
- defaults
dependencies:
- python=3.14
- ipython
- pandas
- pip
- pip:
  - python-pptx
  - openpyxl
EOF
```

### Create Conda environment using environment.yml config file

```sh
conda env create -f environment.yml
```

### Update environement (e.g. if environment.yml needs to be amended)

```sh
conda env update -f environment.yml
```

### Activate environment

```sh
conda activate tesa
```

## Claude

### Create .claude

```sh
mkdir -p .claude
```