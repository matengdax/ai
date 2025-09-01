# macOS & Kubernetes & 代理实用说明

---

## 1. macOS 常用 socket 相关命令

### 1.1 lsof
查看哪些进程监听哪些端口：
```sh
lsof -iTCP -sTCP:LISTEN -n -P
```

### 1.2 netstat
显示网络连接、路由表等（部分 macOS 版本已弃用）：
```sh
netstat -an | grep LISTEN
```

### 1.3 nc (netcat)
建立 socket 连接、测试端口等：
```sh
# 测试端口连通性
nc -vz 127.0.0.1 80

# 作为监听服务器
nc -lk 12345
```

### 1.4 环境变量（ALL_PROXY）
大部分命令行工具可通过环境变量走 SOCKS5 代理：
```sh
export ALL_PROXY=socks5://127.0.0.1:1080
```

---

## 2. macOS 命令行使用 SOCKS5 代理

### 2.1 curl 示例
```sh
curl --socks5 127.0.0.1:1080 https://www.google.com
```

### 2.2 环境变量通用法
```sh
export ALL_PROXY=socks5://127.0.0.1:1080
```
加到 `~/.zshrc` 或 `~/.bash_profile` 可实现永久生效。

### 2.3 git 走 SOCKS5
```sh
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

### 2.4 proxychains-ng 工具
1. 安装
   ```sh
   brew install proxychains-ng
   ```
2. 配置
   编辑 `/usr/local/etc/proxychains.conf`，添加：
   ```
   socks5  127.0.0.1 1080
   ```
3. 使用
   ```sh
   proxychains4 curl https://www.google.com
   ```

---

## 3. chains-ng、chain、chains、ng 含义说明

- **chain**：链条（单数）
- **chains**：链条（复数，多条链）
- **ng**：Next Generation（下一代）
- **chains-ng**：多链条（或链式功能）的下一代版
- **proxychains-ng**：proxychains 的 Next Generation（新一代）版本

---

## 4. macOS 移到废纸篓快捷键

- 快捷键：`Command (⌘) + Delete (⌫)`
- 在 Finder 选中文件后按下即可移到废纸篓。
- 彻底清空废纸篓：`Command + Shift + Delete`

---

## 5. kubernet 和 kubernets 分别是什么意思

- **kubernet**：拼写错误，无独立含义，正确应为 Kubernetes。
- **kubernets**：拼写错误，无独立含义，正确应为 Kubernetes。
- **Kubernetes**：开源容器编排平台，简称 k8s。

---

## 6. kubernets 是什么单词的组合

- 正确应为 **Kubernetes**，源自希腊语 **κυβερνήτης**（kubernētēs），意为“舵手”“领航员”。
- “kubernets” 并非真实单词，仅为误拼写。

---

## 7. macOS 如何访问 iPad 里的文件夹

### 7.1 用 Finder 通过数据线连接
- 用数据线连 iPad 与 MacBook。
- Finder 左侧栏点击 iPad，可访问“文件”App中“在我的 iPad 上”文件夹。

### 7.2 用 AirDrop
- 在 iPad 上选中文件，点分享，选 AirDrop 发送到 Mac。

### 7.3 用 iCloud Drive 或其他云盘
- iPad 文件移到 iCloud Drive，在 Mac 上同账号即可访问。

### 7.4 用第三方 App（如 Documents）
- Documents by Readdle 提供 Wi-Fi 传输功能，iPad 启动后浏览器输入对应地址即可访问。

---

## 8. macOS 有剪切这个选项吗

- **Finder 没有直接“剪切”选项**，但可以用“移动”实现类似功能。
- 方法：选中文件 Command + C，目标文件夹 Command + Option + V（移动/剪切效果）。
- 仅 Command + V 是复制。

---
