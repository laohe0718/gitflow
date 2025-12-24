安装 Git Flow 运行环境

---

## ✅ 第一步：准备环境（Windows）

> 目标：在 Windows 上通过 Git for Windows 安装 `git-flow AVH Edition`，使其可在 PowerShell 或 Git Bash 中使用。

### 1. 确保已安装 Git for Windows
打开 **PowerShell**，运行：
```powershell
git --version
```
✅ 正常输出示例：
```
git version 2.43.0.windows.1
```
> 如果未安装，请先从 [https://git-scm.com/download/win](https://git-scm.com/download/win) 下载并安装（安装时勾选 **"Add Git to PATH"**）。

---

### 2. 打开 Git Bash 并安装 Git Flow

1. 在开始菜单搜索并打开 **Git Bash**
2. 在 Git Bash 窗口中执行以下命令：

```bash
# 下载并运行官方安装脚本（AVH 增强版）
curl -sL https://raw.githubusercontent.com/petervanderdoes/gitflow-avh/develop/contrib/gitflow-installer.sh | bash
```

> 安装过程中会提示：
> ```
> Do you want to install git-flow? [Y/n]
> ```
> 直接按 **回车**（表示 Yes）。

---

### 3. 验证安装成功

仍在 **Git Bash** 中运行：
```bash
git flow version
```

✅ 成功输出示例：
```
1.12.3 (AVH Edition)
```

> ✅ 至此，Git Flow 已安装完成。你可以在 **PowerShell** 或 **Git Bash** 中使用 `git flow` 命令。

---
