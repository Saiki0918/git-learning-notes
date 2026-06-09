# Git 学习笔记 (实战版)

## 1. 基础环境搭建
- **安装配置**
    - 设置名字: `git config --global user.name "Your Name"`
    - 设置邮箱: `git config --global user.email "email@example.com"`
- **创建仓库**
    - 初始化本地库: `git init`
    - 克隆远程库: `git clone <url>`

## 2. 日常开发流程 (标准循环)
- **第一步：同步最新代码**
    - 拉取并合并: `git pull origin master`
    - 仅抓取不合并: `git fetch origin`
- **第二步：修改文件**
    - 查看状态: `git status`
    - 查看差异: `git diff`
- **第三步：提交更改**
    - 添加到暂存区: `git add .` (全部) 或 `git add <file>`
    - 提交到版本库: `git commit -m "描述信息"`
- **第四步：推送到远程**
    - 推送分支: `git push origin master`

## 3. 常见异常处理 (救火指南)
- **场景一：改错了文件，还没 Add**
    - 丢弃工作区的修改: `git checkout -- <file>`
    - *注意：这是危险操作，无法恢复*
- **场景二：Add 错了，还没 Commit**
    - 撤销暂存: `git reset HEAD <file>`
    - *之后可重新 checkout 或重新 add*
- **场景三：Commit 错了，想重来**
    - 撤销最近一次提交(保留修改): `git reset --soft HEAD^`
    - 彻底回退到上一版本: `git reset --hard HEAD^`
- **场景四：误删了文件**
    - 从版本库恢复: `git checkout -- <file>`

## 4. 分支管理策略
- **创建与切换**
    - 创建并切换: `git checkout -b dev`
    - 查看分支: `git branch`
- **合并分支**
    - 普通合并(Fast Forward): `git merge dev`
    - 强制生成合并记录(推荐): `git merge --no-ff -m "merge with no-ff" dev`
- **解决冲突**
    - 现象: 提示 `CONFLICT (content)`
    - 步骤 1: 打开文件手动修改冲突内容
    - 步骤 2: `git add <file>`
    - 步骤 3: `git commit -m "fix conflict"`
- **临时 stash (现场保护)**
    - 场景: 正在修 Bug，手头工作未完成不能提交
    - 储藏现场: `git stash`
    - 恢复现场: `git stash pop`

## 5. 团队协作规范
- **关联远程库**
    - 添加远程: `git remote add origin git@github.com:user/repo.git`
    - 查看远程: `git remote -v`
- **多人协作流程**
    - 1. 尝试推送: `git push origin branch-name`
    - 2. 若失败(别人已推送): `git pull`
    - 3. 若有冲突: 本地解决冲突 -> `git add` -> `git commit`
    - 4. 再次推送: `git push origin branch-name`
- **标签管理 (发布版本)**
    - 打标签: `git tag v1.0`
    - 推送标签: `git push origin v1.0`

## 6. 高级技巧
- **变基 (Rebase)**
    - 作用: 让分叉的提交历史变成一条直线
    - 命令: `git rebase`
- **忽略文件 (.gitignore)**
    - 忽略编译文件、系统临时文件等
    - 规则示例: `*.class`, `/target/`
- **别名配置**
    - 简化命令: `git config --global alias.st status`
    - 简化日志: `git config --global alias.lg "log --color --graph..."`