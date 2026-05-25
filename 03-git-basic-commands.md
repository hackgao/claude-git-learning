# 03 - Git 基础命令速查表

## 📝 学习目标
掌握 Git 的基本命令，能够进行日常的版本控制操作。

## 🚀 核心命令

### 1. 仓库初始化与配置

```bash
# 初始化仓库
git init

# 配置用户信息（全局配置）
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 查看配置
git config --list
git config user.name
```

### 2. 文件操作

```bash
# 添加文件到暂存区
git add filename          # 添加单个文件
git add .                 # 添加所有修改的文件
git add -A                # 添加所有文件（包括删除的）

# 查看状态
git status                # 查看仓库状态
git diff                  # 查看工作区与暂存区差异
git diff --cached        # 查看暂存区与上次提交的差异

# 提交更改
git commit -m "提交信息"    # 提交并添加信息
git commit -am "提交信息"   # 跳过暂存区直接提交

# 删除文件
git rm filename          # 从工作区和暂存区删除
git rm --cached filename # 仅从暂存区删除（保留工作区）
```

### 3. 分支管理

```bash
# 查看分支
git branch               # 查看本地分支
git branch -r            # 查看远程分支
git branch -a            # 查看所有分支

# 创建分支
git branch branch-name    # 创建新分支
git checkout -b branch-name # 创建并切换到新分支

# 切换分支
git checkout branch-name  # 切换到指定分支
git main                 # 快速切换到主分支（如果主分支叫 main）

# 合并分支
git checkout main
git merge branch-name     # 将分支合并到当前分支

# 删除分支
git branch -d branch-name # 删除已合并的分支
git branch -D branch-name # 强制删除分支（未合并的）

# 远程分支操作
git remote -v            # 查看远程仓库
git remote add origin <url> # 添加远程仓库
git push -u origin branch-name # 推送分支并设置上游
```

### 4. 提交历史管理

```bash
# 查看提交历史
git log                  # 查看详细提交历史
git log --oneline        # 查看简化历史（一行一个）
git log --graph          # 图形化显示分支
git log --stat           # 显示每次提交的文件变更统计

# 修改提交
git commit --amend       # 修改最后一次提交
git rebase -i HEAD~3     # 修改最近3次提交（交互式）

# 撤销操作
git reset HEAD~1         # 撤销最后一次提交（保留文件）
git reset --hard HEAD~1  # 撤销最后一次提交（删除文件）
git checkout -- filename  # 恢复文件到最后一次提交的状态
```

### 5. 标签管理

```bash
# 创建标签
git tag v1.0             # 创建轻量标签
git tag -a v1.0 -m "版本1.0" # 创建带注释的标签

# 查看标签
git tag                  # 查看所有标签
git show v1.0           # 查看标签详情

# 推送标签
git push origin v1.0    # 推送单个标签
git push origin --tags  # 推送所有标签
```

## 📋 实战案例

### 案例1：日常开发流程
```bash
# 1. 创建新功能分支
git checkout -b feature/new-login

# 2. 开发代码
git add .
git commit -m "添加登录功能"

# 3. 推送到远程
git push origin feature/new-login

# 4. 合并到主分支（在 PR 中完成）
```

### 案例2：修复紧急 Bug
```bash
# 1. 切换到主分支
git checkout main

# 2. 创建 hotfix 分支
git checkout -b hotfix/fix-login-bug

# 3. 修复问题
git add .
git commit -m "修复登录 Bug #123"

# 4. 快速发布
git tag v1.0.1
git push origin main --tags
```

### 案例3：撤销误操作
```bash
# 如果误提交了敏感信息
git reset --hard HEAD~1
git push --force-with-lease origin main  # 强推（谨慎使用）
```

## 💡 最佳实践

### 1. 提交信息规范
```bash
# 格式：<类型>: <描述>
# 类型：feat, fix, docs, style, refactor, test, chore

# 示例
feat: 添加用户登录功能
fix: 修复登录验证失败的问题
docs: 更新 README 文档
style: 格式化代码
refactor: 重构用户模型
test: 添加登录单元测试
chore: 更新依赖包
```

### 2. 分支命名规范
```bash
# 功能分支：feature/功能名
feature/user-authentication
feature/payment-integration

# 修复分支：fix/问题描述或编号
fix/login-validation
fix/api-timeout-issue

# 发布分支：release/版本号
release/v1.0.0
release/v2.0.0

# 热修复分支：hotfix/问题描述
hotfix/security-patch
```

### 3. Git Flow 工作流
```
main (生产环境)
    ↑
develop (开发环境)
    ↑
├── feature/xxx
├── feature/yyy
└── hotfix/zzz
```

## 🐛 常见问题

### 1. 冲突解决
```bash
# 发生冲突时
git merge feature/new-feature
# 手动解决冲突文件
git add resolved-file
git commit
```

### 2. 远程仓库问题
```bash
# 如果提示权限问题
git remote set-url origin https://new-token@github.com/user/repo.git

# 更新远程分支
git remote update origin --prune
```

### 3. 撤销操作
```bash
# 撤销 add 操作
git reset HEAD filename

# 撤销 commit 但保留修改
git reset --soft HEAD~1

# 完全撤销（包括修改）
git reset --hard HEAD~1
```

## 📚 进阶学习

- [Pro Git Book](https://git-scm.com/book)
- [Atlassian Git Tutorial](https://www.atlassian.com/git)
- [Git Cheatsheet](https://ndpsoftware.com/git-cheatsheet.html)

---

*学习日期: 2026-05-25*
*难度等级: 🟢 初级*
*完成状态: ✅*