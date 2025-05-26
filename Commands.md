# Git 指令大全

> 程序员必备开发工具参考手册

## 目录

1. [全局设置](#全局设置)
2. [常用命令](#常用命令)
3. [分支管理](#分支管理)
4. [远程仓库操作](#远程仓库操作)
5. [撤销与回退](#撤销与回退)
6. [日志与对比](#日志与对比)
7. [完整工作流程](#完整工作流程)

---

## 全局设置

### 配置用户信息
```bash
# 设置全局用户名
git config --global user.name "Your Name"

# 设置全局邮箱地址
git config --global user.email "your.email@example.com"

# 查看所有配置信息
git config --list

# 设置默认分支名为 main
git config --global init.defaultBranch main

# 设置默认编辑器
git config --global core.editor "code --wait"

# 启用颜色输出
git config --global color.ui auto
```

### 配置别名
```bash
# 设置常用命令别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
```

---

## 常用命令

### 仓库初始化
```bash
# 在当前目录初始化 Git 仓库
git init

# 克隆远程仓库
git clone <repository-url>

# 克隆指定分支
git clone -b <branch-name> <repository-url>
```

### 文件操作
```bash
# 查看工作区状态
git status

# 添加所有文件到暂存区
git add .

# 添加指定文件到暂存区
git add <filename>

# 添加所有已跟踪文件的修改
git add -u

# 交互式添加文件
git add -i
```

### 提交操作
```bash
# 提交暂存区文件到本地仓库
git commit -m "commit message"

# 添加并提交已跟踪文件
git commit -am "commit message"

# 修改最近一次提交信息
git commit --amend -m "new commit message"

# 空提交（用于触发CI/CD）
git commit --allow-empty -m "empty commit"
```

---

## 分支管理

### 查看分支
```bash
# 查看本地分支列表
git branch

# 查看远程分支列表
git branch -r

# 查看所有分支（本地+远程）
git branch -a

# 查看分支详细信息
git branch -v
```

### 创建分支
```bash
# 创建新分支
git branch <branch-name>

# 基于指定提交创建分支
git branch <branch-name> <commit-hash>

# 创建并切换到新分支
git checkout -b <branch-name>

# 使用 switch 命令创建并切换分支
git switch -c <branch-name>
```

### 切换分支
```bash
# 切换到指定分支
git checkout <branch-name>

# 使用 switch 命令切换分支
git switch <branch-name>

# 切换到上一个分支
git checkout -

# 切换到主分支
git checkout main
```

### 合并分支
```bash
# 合并指定分支到当前分支
git merge <branch-name>

# 快进合并
git merge --ff-only <branch-name>

# 禁止快进合并（保留合并历史）
git merge --no-ff <branch-name>

# 合并时压缩提交
git merge --squash <branch-name>
```

### 删除分支
```bash
# 删除本地分支
git branch -d <branch-name>

# 强制删除本地分支
git branch -D <branch-name>

# 删除远程分支
git push origin --delete <branch-name>
```

---

## 远程仓库操作

### 远程仓库管理
```bash
# 查看远程仓库信息
git remote -v

# 添加远程仓库
git remote add origin <repository-url>

# 修改远程仓库URL
git remote set-url origin <new-repository-url>

# 重命名远程仓库
git remote rename origin upstream

# 删除远程仓库
git remote remove origin
```

### 推送操作
```bash
# 推送分支到远程仓库
git push origin <branch-name>

# 首次推送主分支并设置上游
git push -u origin main

# 推送所有分支
git push --all origin

# 推送标签
git push --tags origin

# 强制推送（谨慎使用）
git push --force origin <branch-name>
```

### 拉取操作
```bash
# 拉取并合并远程分支到当前分支
git pull

# 拉取指定远程分支
git pull origin <branch-name>

# 获取远程仓库最新状态（不合并）
git fetch

# 获取所有远程分支
git fetch --all

# 拉取时使用变基
git pull --rebase
```

---

## 撤销与回退

### 撤销暂存区
```bash
# 撤销暂存区中的指定文件
git reset HEAD <filename>

# 撤销暂存区中的所有文件
git reset HEAD

# 撤销暂存区（新版本语法）
git restore --staged <filename>
```

### 撤销工作区
```bash
# 撤销工作区中的文件修改
git checkout -- <filename>

# 撤销工作区中所有修改
git checkout -- .

# 撤销工作区修改（新版本语法）
git restore <filename>
```

### 回退提交
```bash
# 撤销最近一次提交，保留修改在暂存区
git reset --soft HEAD~1

# 撤销最近一次提交，保留修改在工作区
git reset --mixed HEAD~1

# 撤销最近一次提交，丢弃所有修改
git reset --hard HEAD~1

# 回退到指定提交
git reset --hard <commit-hash>
```

### 创建反向提交
```bash
# 创建新提交来撤销指定提交
git revert <commit-hash>

# 撤销合并提交
git revert -m 1 <merge-commit-hash>

# 撤销多个提交
git revert <commit-hash1>..<commit-hash2>
```

### 暂存修改
```bash
# 暂存当前工作区修改
git stash

# 暂存包括未跟踪文件
git stash -u

# 暂存时添加描述信息
git stash save "work in progress"

# 查看暂存列表
git stash list

# 恢复最近一次暂存
git stash pop

# 恢复指定暂存
git stash apply stash@{0}

# 删除指定暂存
git stash drop stash@{0}

# 清空所有暂存
git stash clear
```

---

## 日志与对比

### 查看提交历史
```bash
# 查看提交历史
git log

# 以简洁格式查看提交历史
git log --oneline

# 图形化显示分支合并历史
git log --graph --oneline

# 查看所有分支的提交历史
git log --graph --all --oneline

# 查看指定文件的提交历史
git log -- <filename>

# 查看指定作者的提交
git log --author="Author Name"

# 查看指定时间范围的提交
git log --since="2024-01-01" --until="2024-12-31"
```

### 查看提交详情
```bash
# 查看指定提交的详细信息
git show <commit-hash>

# 查看最近一次提交的详细信息
git show HEAD

# 只查看提交信息，不显示差异
git show --stat <commit-hash>
```

### 对比差异
```bash
# 查看工作区与暂存区的差异
git diff

# 查看暂存区与上次提交的差异
git diff --cached

# 查看工作区与上次提交的差异
git diff HEAD

# 对比两个提交之间的差异
git diff <commit-hash1> <commit-hash2>

# 对比两个分支之间的差异
git diff <branch1> <branch2>

# 查看指定文件的差异
git diff <filename>

# 以单词为单位显示差异
git diff --word-diff
```

### 查找和定位
```bash
# 查找包含指定内容的提交
git log --grep="keyword"

# 在代码中搜索
git grep "search-term"

# 查看文件的每一行是谁修改的
git blame <filename>

# 二分查找问题提交
git bisect start
git bisect bad <bad-commit>
git bisect good <good-commit>
```

---

## 完整工作流程

### 1. 项目初始化
```bash
# 创建新项目目录
mkdir my-project
cd my-project

# 初始化Git仓库
git init

# 配置用户信息（如果未全局配置）
git config user.name "Your Name"
git config user.email "your.email@example.com"

# 创建.gitignore文件
echo "node_modules/" > .gitignore
echo "*.log" >> .gitignore
echo ".env" >> .gitignore
```

### 2. 首次提交
```bash
# 创建初始文件
echo "# My Project" > README.md
echo "console.log('Hello World');" > index.js

# 添加文件到暂存区
git add .

# 进行首次提交
git commit -m "Initial commit: Add README and basic setup"

# 检查状态
git status
```

### 3. 连接远程仓库
```bash
# 在GitHub/GitLab等平台创建远程仓库后

# 添加远程仓库
git remote add origin https://github.com/username/my-project.git

# 推送代码到远程仓库
git push -u origin main

# 验证远程连接
git remote -v
```

### 4. 功能开发流程
```bash
# 创建功能分支
git checkout -b feature/user-authentication

# 开发功能...
# 编辑文件，添加新功能

# 查看修改状态
git status

# 添加修改到暂存区
git add src/auth.js src/login.js

# 提交修改
git commit -m "Add user authentication system

- Implement login functionality
- Add password validation
- Create user session management"

# 继续开发和提交...
git add .
git commit -m "Add logout functionality"

# 推送功能分支到远程
git push origin feature/user-authentication
```

### 5. 更新和同步
```bash
# 切换到主分支
git checkout main

# 拉取最新代码
git pull origin main

# 切换回功能分支
git checkout feature/user-authentication

# 将主分支的最新修改合并到功能分支
git rebase main

# 如果有冲突，解决冲突后继续
# 编辑冲突文件...
git add <conflicted-files>
git rebase --continue

# 推送更新后的功能分支
git push --force-with-lease origin feature/user-authentication
```

### 6. 代码审查和合并准备
```bash
# 压缩多个提交为一个（如果需要）
git rebase -i HEAD~3

# 在交互界面中选择 squash 或 fixup

# 推送最终版本
git push --force-with-lease origin feature/user-authentication

# 在GitHub/GitLab创建Pull Request/Merge Request
```

### 7. 合并与冲突处理
```bash
# 方式一：通过命令行合并
git checkout main
git pull origin main
git merge feature/user-authentication

# 如果有合并冲突
# 1. 查看冲突文件
git status

# 2. 手动编辑冲突文件，解决冲突标记
# <<<<<<< HEAD
# =======
# >>>>>>> feature/user-authentication

# 3. 标记冲突已解决
git add <resolved-files>

# 4. 完成合并
git commit -m "Resolve merge conflicts in user authentication"

# 方式二：使用变基合并（保持线性历史）
git checkout main
git pull origin main
git checkout feature/user-authentication
git rebase main
git checkout main
git merge feature/user-authentication
```

### 8. 推送与清理
```bash
# 推送合并结果到远程主分支
git push origin main

# 删除本地功能分支
git branch -d feature/user-authentication

# 删除远程功能分支
git push origin --delete feature/user-authentication

# 清理本地分支引用
git remote prune origin

# 创建版本标签（如果需要）
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

### 9. 持续开发循环
```bash
# 开始新功能开发
git checkout main
git pull origin main
git checkout -b feature/payment-system

# 重复步骤4-8...
```

### 10. 紧急修复流程
```bash
# 基于main分支创建热修复分支
git checkout main
git pull origin main
git checkout -b hotfix/security-patch

# 进行紧急修复
# 编辑代码...

# 快速提交和推送
git add .
git commit -m "Security patch: Fix authentication vulnerability"
git push origin hotfix/security-patch

# 快速合并到main（跳过正常审查流程）
git checkout main
git merge hotfix/security-patch
git push origin main

# 同时合并到开发分支（如果存在）
git checkout develop
git merge hotfix/security-patch
git push origin develop

# 清理热修复分支
git branch -d hotfix/security-patch
git push origin --delete hotfix/security-patch

# 创建紧急版本标签
git tag -a v1.0.1 -m "Emergency security patch"
git push origin v1.0.1
```

---

## 高级技巧

### 配置文件示例
```bash
# ~/.gitconfig 全局配置示例
[user]
    name = Your Name
    email = your.email@example.com

[core]
    editor = code --wait
    autocrlf = input
    ignorecase = false

[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    last = log -1 HEAD
    visual = !gitk
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

[color]
    ui = auto

[push]
    default = simple

[pull]
    rebase = false