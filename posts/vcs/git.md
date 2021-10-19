---
layout: post
title: Git
date: 2021-10-10
---

## git config

```bash
# 用户信息(必须配置)
git config --global user.name "redbg"
git config --global user.email redbg@softsec.org

# 使用编辑器打开配置文件
git config --global --edit

# Configure default branch name
git config --global init.defaultBranch main

# Configure default editor
git config --global core.editor code
```

```bash
# 查看所有配置
git config --list

# 查看所有配置以及它们来自哪个文件
git config --list --show-origin

# [Windows] C:\Program Files\Git\etc\gitconfig
# $(prefix)/etc/gitconfig
git config --system --list

# ~/.gitconfig
git config --global --list

# .git/config
git config --local --list

# git config --show-origin <key>
git config --show-origin user.name
```

## git init & git clone

```bash
# 创建一个本地仓库
git init

# 克隆一个远程仓库
git clone https://github.com/redbg/softsec.git
```

## git add

### .gitignore

## git status

```bash
# 检查文件状态
git status

# 检查文件状态(紧凑信息)
git status -s
git status --short
```

### 三个区域

- 工作区
- 暂存区
  - 暂存区是一个文件`.git/index`，包含在Git目录中，它存储了下一次提交需要的信息。
- Git目录
  - Git目录是Git存储项目元数据和对象数据库的地方。

![Working tree, staging area, and Git directory](/assets/images/areas.png)

```bash
echo "# 111" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main

# Working                    # 工作区
# │  README.md               # "# 111"
# │
# └─.git                     # Git目录
#     │  COMMIT_EDITMSG      # `git commit` 默认打开的文件
#     │  config              # `git config --local --list`
#     │  description
#     │  HEAD                # 指向当前分支 (HEAD -> refs/heads/main) `git log`
#     │  index               # 暂存区 `git ls-files --stage`
#     │
#     ├─info
#     │      exclude
#     │
#     ├─logs
#     │  │  HEAD             # `git reflog`
#     │  │
#     │  └─refs
#     │      └─heads
#     │              main    # `git reflog main`
#     │
#     ├─objects
#     │  ├─11                # `git cat-file -t 1122` = commit
#     │  │      22...        # `git cat-file -p 1122` = tree 3344..., parent 0000..., author, committer, "first commit"
#     │  │
#     │  ├─33                # `git cat-file -t 3344` = tree
#     │  │      44...        # `git cat-file -p 3344` = 100644, blob, 5566..., README.md
#     │  │
#     │  ├─55                # `git cat-file -t 5566` = blob
#     │  │      66...        # `git cat-file -p 5566` = "# 111"
#     │  │
#     │  ├─info
#     │  └─pack
#     └─refs
#         ├─heads
#         │      main        # (main -> 1122...) `git log main`
#         │
#         └─tags
```

### 文件状态

![The lifecycle of the status of your files](/assets/images/lifecycle.png)
