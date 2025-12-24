
## ✅ 修复 v1.0.2 版本 bug 的完整步骤

> 💡 **前提**：`v1.0.2` 已发布，现在需要紧急修复生产环境的 bug

---

### 🏷️ 1. 确认当前版本标签

```powershell
# 查看所有标签
git tag -l
```

✅ 输出示例：
```
v1.0.0
v1.0.1
v1.0.2
```

---

### 🛠️ 2. 从 v1.0.2 标签创建热修复分支

```powershell
# 基于 v1.0.2 创建热修复分支
git flow hotfix start v1.0.3 v1.0.2

# 确保 main 是最新的(如何git flow hotfix start v1.0.3 v1.0.2 一直报错就采用下面这个方案)
git checkout main
git pull origin main

# 从当前 main 创建热修复分支
git flow hotfix start v1.0.3

```

> 💡 参数说明：
> - `v1.0.3`：即将发布的修复版本号
> - `v1.0.2`：基于哪个标签创建（修复的目标版本）

✅ 输出：
```
Switched to a new branch 'hotfix/v1.0.3'
```

> 📌 热修复分支会从 `v1.0.2` 标签创建，**不包含 `develop` 上的新功能**

---

### 🐛 3. 修复 bug

```powershell
添加文件 git flow create fix branch.md
```

---

### ✍️ 4. 提交修复代码

```powershell
# 添加修复文件
git add git flow create fix branch.md

# 提交修复（使用 fix 类型）
git commit -m "fix: add git flow create fix branch in v1.0.3"
```

> 💡 提交信息格式：`fix(scope): description`

---

### 🧪 5. 测试修复（可选但推荐）

```powershell
# 运行测试确保修复有效
# npm test  # 或其他测试命令
```

---

### ☁️ 6. 推送热修复分支到 GitHub（用于备份或协作）

```powershell
# 推送热修复分支到远程
git push -u origin hotfix/v1.0.3
```

---

### 🎯 7. 完成热修复（合并到 main 和 develop）

```powershell
# 完成热修复（会自动合并到 main 和 develop，并创建 v1.0.3 标签）
git flow hotfix finish v1.0.3
```

> 这一步会：
> 1. 将 `hotfix/v1.0.3` 合并到 `main`
> 2. 在 `main` 上创建 `v1.0.3` 标签
> 3. 将 `hotfix/v1.0.3` 合并到 `develop`
> 4. 删除 `hotfix/v1.0.3` 分支

---

### ☁️ 8. 推送所有变更到 GitHub

```powershell
# 推送 main（包含 bug 修复）
git checkout main
git push origin main

# 推送 develop（同步修复内容）
git checkout develop
git push origin develop

# 推送标签
git push origin --tags
```

---

### ✅ 9. 验证修复结果

```powershell
# 查看标签
git tag -l
# 应包含：v1.0.3

# 查看 main 分支的最新提交
git log --oneline -5 main
# 应包含热修复提交

# 查看远程分支
git branch -r
# 应显示 origin/main, origin/develop
```

---

### 📊 10. 部署到生产环境

> 🚀 现在可以：
> - 从 `main` 分支部署 `v1.0.3` 到生产环境
> - 或基于 `v1.0.3` 标签进行部署

---

## 🚨 注意事项

| 情况 | 处理方式 |
|------|----------|
| 修复多个 bug | 在同一个 hotfix 分支中修复多个 bug |
| 需要团队协作 | 使用 Pull Request 进行 Code Review |
| 修复失败 | 用 `git flow hotfix delete v1.0.3` 删除 |
| 修复后测试不通过 | 在 hotfix 分支上继续修复，直到通过 |

---
## 🎯 总结

| 步骤 | 命令 | 目的 |
|------|------|------|
| 1. 准备 | `git tag -l` | 确认目标版本 |
| 2. 创建 | `git flow hotfix start v1.0.3 v1.0.2` | 基于标签创建修复分支 |
| 3. 修复 | `git add && git commit` | 实现修复并提交 |
| 4. 推送 | `git push -u origin hotfix/v1.0.3` | 同步到远程 |
| 5. 合并 | `git flow hotfix finish v1.0.3` | 合并到 main/develop 并打标签 |
| 6. 同步 | `git push origin --tags` | 推送标签到 GitHub |

现在你已经掌握了在 Git Flow 中**修复生产版本 bug 的完整流程**！这种热修复方式确保了生产环境的稳定性，同时保持了代码历史的清晰性。