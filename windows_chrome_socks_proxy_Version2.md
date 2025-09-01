# Windows 用命令行启动 Chrome 并设置 SOCKS 代理

## 步骤

1. **找到 Chrome 可执行文件路径**  
   通常路径如下：
   ```
   "C:\Program Files\Google\Chrome\Application\chrome.exe"
   ```
   或
   ```
   "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"
   ```

2. **打开命令提示符（cmd）**

3. **用命令行启动 Chrome 并设置 SOCKS 代理**  
   假设你的 SOCKS5 代理在本地 1080 端口：

   ```cmd
   "C:\Program Files\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://127.0.0.1:1080"
   ```
   或
   ```cmd
   "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --proxy-server="socks5://127.0.0.1:1080"
   ```

## 说明

- 此命令只影响当前启动的 Chrome 实例。
- 你可以将命令写入 `.bat` 脚本，双击运行。
- 支持 HTTP/SOCKS4/SOCKS5 代理，例如：
  - `--proxy-server="socks5://127.0.0.1:1080"`
  - `--proxy-server="http://127.0.0.1:8080"`

## 进阶

- 需要更灵活代理规则，可用 SwitchyOmega 等 Chrome 插件。

---