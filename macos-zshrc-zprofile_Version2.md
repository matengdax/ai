# macOS zsh 设置永久变量

## 1. `.zshrc` 和 `.zprofile` 的区别

- `.zshrc`：每次启动交互式 shell（如新开终端窗口）时加载，适合日常环境变量、别名、函数等。
- `.zprofile`：登录 shell 时加载（如登陆系统或用 `zsh --login`），适合全局环境变量。类似 bash 的 `.profile`。

---

## 2. 没有 `.zshrc` 只有 `.zprofile` 怎么办？

如果你的主目录下**没有 `.zshrc`，只有 `.zprofile`**，可以直接在 `.zprofile` 里设置永久环境变量，方法如下：

### 步骤

1. 编辑 `.zprofile` 文件：

   ```bash
   nano ~/.zprofile
   ```

2. 添加环境变量，例如：

   ```bash
   export ALL_PROXY=socks5://127.0.0.1:1080
   export PATH="$HOME/bin:$PATH"
   export LANG="zh_CN.UTF-8"
   ```

3. 保存并退出（nano 用 `Ctrl+O` 保存，`Ctrl+X` 退出）。

4. 让更改立即生效：

   ```bash
   source ~/.zprofile
   ```

   或关闭终端重新打开。

---

## 3. 建议

- `.zprofile`、`.zshrc` 都可以设置永久变量，日常建议放 `.zshrc`，但 `.zprofile` 也没问题。
- 两者都存在时，日常变量放 `.zshrc`，登录相关变量放 `.zprofile`。

---