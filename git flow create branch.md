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
# 合并 feature/create-branch 到 develop，并删除本地和远程分支
git flow feature finish create-branch
```

> ⚠️ 此命令不会推送！

### 推送更新后的 develop 分支：

```powershell
git checkout develop
git push
```



### ✅ 最终验证

```powershell
# 查看当前分支
git branch
# 应显示：* develop

# 查看远程分支
git branch -r
# 应包含 origin/main, origin/develop
```



## ✅ 将 develop 合并到 main 的完整步骤

> 💡 **前提**：`develop` 分支已经包含了所有准备发布的功能（如你已完成 `feature/create-branch` 并合并回 `develop`）

---

### 🚀 1. 确保 develop 分支是最新的

```powershell
# 切换到 develop 分支
git checkout develop

# 拉取最新远程内容
git pull origin develop
```

---

### 📦 2. 开始发布分支（Git Flow 标准流程）

```powershell
# 创建发布分支（例如：v1.0.0）
git flow release start v1.0.0
```

> 这会从 `develop` 创建 `release/v1.0.0` 分支，用于：
> - 最后的测试
> - 修复发布前的 bug
> - 准备版本说明

---

### 🧪 3. （可选）在发布分支上进行最后测试/修复

```powershell
# 例如：添加版本说明文件
@"
# 版本 v1.0.0 发布说明

## 新增功能
- 用户身份验证模块 (feature/create-branch)
- 手机号+验证码登录

## 修复
- 无
"@ | Out-File -Encoding UTF8 RELEASE_NOTES.md

# 提交
git add RELEASE_NOTES.md
git commit -m "docs: add release notes for v1.0.0"
```

---

### 🎯 4. 完成发布（合并到 main 和 develop，并打标签）

```powershell
# 完成发布（会自动合并到 main 和 develop，并打 v1.0.0 标签）
git flow release finish v1.0.0
```

> 这一步会：
> 1. 将 `release/v1.0.0` 合并到 `main`
> 2. 在 `main` 上创建 `v1.0.0` 标签
> 3. 将 `release/v1.0.0` 合并到 `develop`
> 4. 删除 `release/v1.0.0` 分支

---

### ☁️ 5. 推送所有变更到 GitHub

```powershell
# 推送 main（包含新合并的内容）
git checkout main
git push origin main

# 推送 develop（同步发布内容）
git checkout develop
git push origin develop

# 推送标签
git push origin --tags
```

---

### 📊 6. 验证合并结果

```powershell
# 查看分支状态
git branch -a

# 查看标签
git tag -l

# 查看 main 分支的最新提交
git log --oneline -5 main
```

✅ 你应该看到：
- `main` 和 `develop` 分支内容一致（或 `main` 包含 `develop` 的所有内容）
- 存在 `v1.0.0` 标签
- GitHub 上 `main` 和 `develop` 都已更新

---

## 🔄 简化版（直接合并，不走发布流程）

> ❗ **不推荐**，但如果你不需要 Git Flow 的发布管理，可以：

```powershell
# 切换到 main
git checkout main

# 拉取最新内容
git pull origin main

# 合并 develop
git merge develop --no-ff -m "merge develop into main for release"

# 推送 main
git push origin main
```

> ⚠️ 这种方式**不会创建发布标签**，也不符合 Git Flow 标准。

---

## 📌 最佳实践总结

| 操作 | 推荐方式 | 原因 |
|------|----------|------|
| `develop` → `main` | `git flow release` | 标准 Git Flow，支持版本管理 |
| 版本标记 | `v1.0.0` 标签 | 便于回溯、CI/CD 集成 |
| 推送顺序 | `main` → `develop` → `tags` | 确保一致性 |
| 协作 | 使用 Pull Request | 代码审查、变更记录 |

---

现在你已经成功将 `develop` 的内容合并到 `main`，并按照 Git Flow 标准完成了版本发布！🎉

如果需要配置 GitHub Actions 自动化发布流程，也可以继续问我 😊

## 📌 总结

此文档包含从 `git init` 到 `git flow feature finish` 全流程，含 GitHub 推送



