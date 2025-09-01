# VS Code reStructuredText 扩展报错解决方法

## 报错内容

```
Command failed: "python" -c "import sys; print(sys.version_info[0])"
/bin/sh: python: command not found
```

## 分析

- 扩展需要 Python 运行环境，但你的 macOS 下没有 `python` 命令（新版 macOS 默认无 Python）。
- reStructuredText 扩展还需要 Microsoft Python、reStructuredText Syntax Highlighting、Esbonio 三个 VS Code 扩展。

---

## 解决步骤

### 1. 安装 Python

用 Homebrew 安装最新版 Python：

```bash
brew install python
```

一般会有 `python3`，如需 `python` 命令，建立软链接：

```bash
ln -sfn /opt/homebrew/bin/python3 /opt/homebrew/bin/python
```

### 2. 安装 VS Code 所需扩展

在扩展市场依次安装：

- Python （ms-python.python）
- reStructuredText Syntax Highlighting（trond-snekvik.simple-rst）
- Esbonio（swyddfa.esbonio）

### 3. 检查 VS Code 终端环境

在 VS Code 终端中输入：

```bash
python --version
python3 --version
```

确认已安装且可用。

### 4. 重启 VS Code

---

## 总结

- 安装 Python 并确保有 `python` 命令。
- 安装所有所需扩展。
- 检查 VS Code 终端环境变量设置。

---