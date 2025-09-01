# macOS Chrome 设置代理服务器

## 说明

- **Chrome 浏览器本身没有独立的代理服务器设置界面**，它默认使用 macOS 系统的网络代理设置。
- 你可以通过系统偏好设置（系统设置）配置代理，Chrome 会自动跟随。

---

## 方法一：通过系统设置配置代理

1. 打开 **系统设置**（或“系统偏好设置”）。
2. 进入 **网络**。
3. 选择你正在使用的网络（如 Wi-Fi）。
4. 点击右下角的 **详情...** 或 **高级...**。
5. 找到 **代理**（Proxies）标签页。
6. 勾选需要的代理类型（如 SOCKS 代理、HTTP 代理等），填写服务器与端口（如 `127.0.0.1:1080`）。
7. 应用并保存。

> **注意**：这样设置后，所有使用系统代理的程序（包括 Chrome）都会走该代理。

---

## 方法二：命令行临时启动 Chrome 并指定代理

```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --proxy-server="socks5://127.0.0.1:1080"
```

- 仅影响用此命令启动的 Chrome 实例，其他程序不受影响。

---

## 方法三：使用 Chrome 扩展插件（如 SwitchyOmega）

- 适合需要灵活切换代理，或只想让部分网站走代理时使用。
- 搜索安装 [SwitchyOmega](https://chrome.google.com/webstore/detail/switchyomega/padekgcemlokbadohgkifijomclgjgif) 并按照指引配置。

---

## 总结

- 推荐直接设置 macOS 系统代理，Chrome 会跟随。
- 只想让 Chrome 走代理可用命令行参数。
- 需多策略切换时用插件。

---