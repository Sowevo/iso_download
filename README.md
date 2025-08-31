## JSON文件格式

`distributions.json` 文件包含以下结构：

```json
{
  "distributions": [
    {
      "distribution": "发行版名称",
      "type": "操作系统类型",
      "download_url": "下载链接",
      "checksum_url": "校验和文件链接",
      "checksum": "SHA256校验和"
    }
  ]
}
```

### 支持的操作系统类型

- **linux**: Linux发行版（当前支持）
- **windows**: Windows系统（未来支持）
- **macos**: macOS系统（未来支持）

## 使用方法

### 默认行为

```bash
# 直接运行脚本，默认下载所有发行版
python download_linux.py

# 可以与其他参数组合使用
python download_linux.py --download-dir "/custom/path"
python download_linux.py --json-file "my_distributions.json"
python download_linux.py --no-verify
python download_linux.py --download-dir "/custom/path" --no-verify
```

### 1. 查看可用的发行版

```bash
# 列出所有发行版
python download_linux.py --list

# 按名称过滤
python download_linux.py --list --filter-name "Ubuntu"

# 按类型过滤
python download_linux.py --list --filter-type "linux"
```

### 2. 下载特定发行版

```bash
# 下载Ubuntu
python download_linux.py --download "Ubuntu"

# 跳过校验和验证
python download_linux.py --download "Ubuntu" --no-verify
```

### 3. 下载所有发行版

```bash
# 下载所有发行版（需要较长时间）
python download_linux.py --download-all

# 跳过校验和验证
python download_linux.py --download-all --no-verify
```

### 4. 使用自定义JSON文件

```bash
python download_linux.py --json-file "my_distributions.json" --list
```

### 5. 指定下载目录

```bash
# 指定自定义下载目录
python download_linux.py --download "Ubuntu" --download-dir "/path/to/downloads"

# 默认下载到脚本所在目录
python download_linux.py --download "Ubuntu"
```

## 校验和验证

脚本支持智能校验和验证，按以下优先级进行：

1. **checksum_url**: 从URL获取最新的校验和
2. **checksum**: 使用JSON中存储的校验和
3. **跳过验证**: 如果两者都没有，则跳过验证

### 支持的校验和格式

- **标准格式**: `checksum filename`
- **PGP签名格式**: `SHA256 (filename) = checksum` (如Fedora使用的格式)

## 下载目录结构

下载的文件将保存在指定目录下，按类型和发行版名称组织：

```
linux/
├── Ubuntu/
│   ├── ubuntu-25.04-desktop-amd64.iso
│   └── ubuntu-25.04-live-server-amd64.iso
├── CentOS/
│   └── CentOS-Stream-9-latest-x86_64-dvd1.iso
└── ...
```

