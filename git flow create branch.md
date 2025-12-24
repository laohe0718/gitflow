创建新分支并提交全流程

## ✅ 第二步：创建并完成 feature/create-branch（从零到推送到 GitHub）

> 目标：初始化项目 → 关联 GitHub → 创建功能分支 → 添加内容 → 提交 → 推送 → 完成功能

> 💡 **所有命令在 PowerShell 中执行**（确保 Git 已加入系统 PATH）

---

### 📁 1. 创建项目目录并初始化 Git 仓库

```powershell
# 进入工作区
cd D:\WorkSpace\Study

# 创建新项目文件夹
mkdir gitflow
cd gitflow

# 初始化 Git 仓库
git init
```

---

### ⚙️ 2. 初始化 Git Flow（使用默认配置）

```powershell
git flow init
```

> 按以下方式交互（直接回车，仅标签前缀输入 `v`）：

```text
Branch name for production releases: [main]              ← 回车
Branch name for "next release" development: [develop]   ← 回车
Feature branches? [feature/]                            ← 回车
Bugfix branches? [bugfix/]                              ← 回车
Release branches? [release/]                            ← 回车
Hotfix branches? [hotfix/]                              ← 回车
Support branches? [support/]                            ← 回车
Version tag prefix? []                                  ← 输入 v 再回车
Hooks and filters directory? [...]                      ← 回车
```

> ✅ 此时自动创建 `develop` 分支，并回到 `main`。对于已经在git lab 中创建好的项目就没有此过程

---

### 🔗 3. 在 GitHub 创建空仓库（手动操作）

1. 登录 [GitHub](https://github.com)
2. 点击右上角 **「+」→ New repository**
3. 仓库名：`gitflow`
4. **不要勾选任何初始化选项（README/.gitignore/License）**
5. 点击 **Create repository**

> 记下仓库地址，例如：  
> `https://github.com/laohe0718/gitflow.git`

---

### 🌐 4. 关联本地仓库与 GitHub

```powershell
# 替换 yourname 为你的 GitHub 用户名
git remote add origin https://github.com/laohe0718/gitflow.git
```

---

### 📤 5. 推送初始分支（main + develop）

```powershell
# 推送 main
git checkout main
git push -u origin main

# 推送 develop
git checkout develop
git push -u origin develop
```

✅ 输出应包含：
```
branch 'main' set up to track 'origin/main'.
branch 'develop' set up to track 'origin/develop'.
```

---

### 🌱 6. 创建功能分支 `feature/create-branch`

```powershell
git flow feature start create-branch
```

✅ 输出：
```
Switched to a new branch 'feature/create-branch'
```

> 当前位于 `feature/create-branch` 分支。

---

### ✍️ 7. 添加新内容并提交

```powershell
# 创建功能说明文件
@"
# 功能：laohe0718
- 实现用户身份验证模块
- 支持手机号+验证码登录
- 前端页面原型设计
"@ | Out-File -Encoding UTF8 feature_spec.md

# 提交更改
git add feature_spec.md
git commit -m "feat(laohe0718): add feature specification"
```

---

### ☁️ 8. 推送功能分支到 GitHub（用于备份或协作）

```powershell
git push -u origin feature/create-branch
```

> ✅ 现在 GitHub 上可以看到 `feature/create-branch` 分支。

---

### 🎯 9. 完成功能（合并回 develop 并清理）

```powershell
# 合并 feature/create-branch 到 develop，并删除本地分支
git flow feature finish create-branch
```

> ⚠️ 此命令不会推送！

### 推送更新后的 develop 分支：

```powershell
git checkout develop
git push
```

### （可选）删除远程 feature 分支：

```powershell
git push origin --delete feature/create-branch
```

---

### ✅ 最终验证

```powershell
# 查看当前分支
git branch
# 应显示：* develop

# 查看远程分支
git branch -r
# 应包含 origin/main, origin/develop
```

---

## 📌 总结

| 步骤 | 内容 |
|------|------|
| **第一步** | 通过 Git Bash 安装 `git-flow AVH`，验证版本 |
| **第二步** | 从 `git init` 到 `git flow feature finish` 全流程，含 GitHub 推送 |



