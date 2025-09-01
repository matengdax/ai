## 恢复 `.yum_repository.yml.swp` 文件

### 步骤

1. **备份**
   ```bash
   cp .yum_repository.yml.swp /tmp/yum_repository.swp.bak
   ```

2. **查看可恢复内容**
   ```bash
   vim -r
   ```
   - 列出所有可恢复的 swap 文件。
   - 或直接恢复：
     ```bash
     vim -r .yum_repository.yml
     ```

3. **恢复文件**
   - 如果 Vim 提示有 swap 文件：
     - 按 `R`（大写）进入恢复模式。
   - 进入后保存并退出：
     ```bash
     :w
     :q
     ```

4. **原文件已删除**
   - 若原文件不存在，也可通过以下命令恢复：
     ```bash
     vim -r .yum_repository.yml
     ```
   - 保存为新文件。

5. **删除旧 swap 文件**
   ```bash
   rm .yum_repository.yml.swp
   ```

### 辅助命令

- **仅查看 swap 内容：**
  ```bash
  strings .yum_repository.yml.swp | less
  ```

- **强制恢复：**
  ```bash
  vim -r .yum_repository.yml.swp
  ```

### 注意事项

- **恢复后确认：** 重新用 `vim` 打开文件，若不再提示 swap 文件，则可安全删除。
- **不要直接修改 swap 文件：** 让 Vim 处理，避免数据损坏。