# pip、pipx 与代理相关常见问题

---

## 1. 如何让 pipx 走 socks5 代理？

方法和 pip 相同，推荐使用环境变量：

```bash
export ALL_PROXY=socks5://127.0.0.1:10808
pipx install 包名
```
用完后可以取消：

```bash
unset ALL_PROXY
```

也可以只对一条命令生效：

```bash
ALL_PROXY=socks5://127.0.0.1:10808 pipx install 包名
```

### 注意
- socks5 代理需要依赖 `pysocks` 包，如遇 `Missing dependencies for SOCKS support`，请先安装：
  ```bash
  python3 -m pip install pysocks
  ```
- pipx 本身不处理代理，实际是把环境变量传递给 pip。

---

## 2. pip install pysocks 和 pipx install pysocks 报 PEP 668 错误

### 背景
- 用 Homebrew 安装的 Python，pip 安装全局包会报错，提示“externally-managed-environment”，并建议参见 PEP 668。
- pipx 不适合安装没有命令行入口的库，比如 pysocks。

### 正确做法
- 推荐**用虚拟环境安装库**：

  ```bash
  python3 -m venv ~/venv-pysocks
  source ~/venv-pysocks/bin/activate
  pip install pysocks
  ```

  用完 deactivate 退出虚拟环境。

- pipx 用于安装有命令行入口的工具，而不是单纯的库。

---

## 3. pysocks 安装在哪里才有效？以后必须激活 venv 吗？

- 如果你只在某个虚拟环境装了 pysocks，只有激活这个虚拟环境时 pip/pipx/python 才能用 SOCKS5。
- pipx 安装的每个命令行工具有自己的隔离环境，需要用 `pipx inject` 给它们加依赖。

  ```bash
  pipx inject 工具名 pysocks
  ```

- 不建议在 Homebrew Python 全局环境用 `--break-system-packages` 装库，有风险。

---

## 4. pip 能走 http 或 https 代理吗？

可以，pip 原生支持 HTTP/HTTPS 代理：

- 命令行参数：

  ```bash
  pip install 包名 --proxy http://127.0.0.1:8888
  pip install 包名 --proxy https://127.0.0.1:8888
  ```

- 环境变量：

  ```bash
  export HTTP_PROXY="http://127.0.0.1:8888"
  export HTTPS_PROXY="http://127.0.0.1:8888"
  pip install 包名
  ```

- 配置文件：

  ```ini
  [global]
  proxy = http://127.0.0.1:8888
  ```

- pip 对 HTTP/HTTPS 代理**不需要额外包**，仅 socks5 才需要 pysocks。

---

## 5. pipx 走 http/https 代理要安装什么包吗？

- **不需要。**
- pipx 走 http/https 代理时，只需设置参数或环境变量，不需要任何第三方库。

---

## 6. pipx 的 inject 是什么？为什么加了库所有命令都能用？

- **inject** 是 pipx 的一个功能，用于向某个命令行工具的隔离环境“注入”额外依赖。
- 原理是 pipx 给每个工具建独立 venv，inject 就是往这个 venv 用 pip 安装新库。
- 这样你可以让某个工具拥有支持 socks5 代理等扩展能力，不影响其它工具。

---

## 7. pipx 不是用来安装库的, pysocks 没有命令行入口, 用 pipx 没意义。怎么理解？

- pipx 用来全局安装**带命令行的 Python 工具**（如 httpie、black、pylint），装完后能直接在终端运行命令。
- “没有命令行入口”的库（如 pysocks、requests、numpy）只提供 import 用，pipx 安装它们后终端不会多出可用命令，没实际意义。
- 不是所有 Python 库都没有命令行，有些（如 black、httpie）既是库也是命令行工具，这种可以用 pipx。

---

## 8. httpie 是做什么的？pipx inject httpie pysocks 有什么用？

- **httpie** 是一个友好的命令行 HTTP 客户端，适合调试、测试 API。
- 用 `pipx install httpie` 后可直接用 `http` 命令。
- 如果你需要 httpie 走 socks5 代理，则需要在 httpie 的虚拟环境里安装 pysocks：

  ```bash
  pipx inject httpie pysocks
  ```

- pipx install pysocks 没意义，因为 pysocks 本身没有命令行入口，仅提供给其它工具调用。

---

## 9. 总结

- pipx 用于安装有命令行入口的 Python 工具。
- inject 可以给这些工具加扩展依赖，比如支持 socks5 代理。
- pip 对 http/https 代理原生支持，无需额外包；socks5 代理需要 pysocks。
- 单纯的 Python 库不要用 pipx 安装，用 pip/venv 即可。