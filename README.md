# 🐳 Docker Registry Explorer

一款功能强大的Docker Registry浏览、下载和安全测试工具，集成了镜像管理、认证爆破、敏感信息搜索等多项实用功能。

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS-green)
![Go](https://img.shields.io/badge/Go-1.22+-00ADD8?logo=go)
![Wails](https://img.shields.io/badge/Wails-v2-red)

---

## ✨ 核心功能

### 🔍 镜像浏览管理

![image-20251106172015745](https://oss.bdziyi.com/biji/202511061720183.png)

- **Registry连接**：支持HTTP/HTTPS，自动保存连接历史

- **Basic Auth认证**：支持需要账号密码的私有Registry

- **仓库浏览**：查看所有仓库列表，支持搜索过滤

- **标签管理**：查看镜像的所有标签版本

- **层查看**：查看镜像的每一层详细信息（大小、digest）

- **批量下载**：勾选仓库/标签/层进行批量下载

- **下载历史**：自动记录所有下载，支持管理和删除（文件同步删除）

  ![image-20251106172046694](https://oss.bdziyi.com/biji/202511061720740.png)

  ![d2e2f7f9866e58e1f25d09dbbba0961d](https://oss.bdziyi.com/biji/202511061722570.png)

### 🛡️ 认证爆破管理

![d09589bf72574be2575df4b3f49fa6cf](https://oss.bdziyi.com/biji/202511061721810.png)

- **多线程爆破**：支持1-100个并发线程
- **自定义字典**：支持用户名和密码字典文件
- **智能延迟**：可调节请求延迟，防止IP被封
- **实时日志**：查看爆破过程和成功的凭证
- **自动填充**：爆破成功后自动填充凭证到镜像浏览区域
- **结果保存**：成功的凭证自动保存到history目录

### 🔎 敏感信息搜索

![ea84bbb258bfe896d5f3a558c5c307da](https://oss.bdziyi.com/biji/202511061721281.png)

- **强大规则库**：25+种内置敏感信息正则表达式
  - 云服务密钥（阿里云、AWS、腾讯云）
  - 数据库凭证（MySQL、Redis、MongoDB、JDBC）
  - 账号密码（中英文支持）
  - 身份证号、手机号、邮箱
  - JWT Token、Basic Auth、Bearer Token
  
- **自动解压**：智能解压压缩包并搜索内容
  - 支持格式：ZIP、TAR、TAR.GZ、JAR、WAR、EAR、GZ
  - Docker镜像层文件（智能检测gzip压缩的tar）
  - 递归解压（最多10层嵌套）
  
- **智能过滤**：200+黑名单规则
  - 过滤代码片段（Java字节码、Python/JavaScript代码）
  - 过滤国际化错误消息
  - 过滤SDK和库文件内容
  - 二进制文件自动检测跳过
  
- **自定义支持**：
  - 自定义正则表达式
  - 自定义文件扩展名
  - 可调节文件大小限制（3MB-500MB或不限制）
  - 支持"仅使用自定义规则"模式
  
- **高性能**：多线程并发搜索，自动跳过不必要的目录

### ⚙️ 系统功能

![db5d5d0702ed37c2da9506fee4bae482](https://oss.bdziyi.com/biji/202511061722032.png)

- **代理支持**：配置HTTP/HTTPS代理，支持代理测试
- **主题切换**：浅色/深色主题
- **下载路径设置**：自定义下载保存位置
- **版本检测**：自动检测更新，提醒用户升级

---

## 🚀 快速开始

### 下载程序

https://github.com/mhtsec/Docker-Registry-exp/releases

支持平台：
- 🍎 macOS (Apple Silicon / Intel)
- 🪟 Windows (x64 / ARM64)
- 🐧 Linux (AMD64)

### 运行程序

#### Windows
双击 `docker-registry-explorer-windows-x64.exe`

#### macOS
1. 解压zip文件
2. 双击 `docker-registry-explorer.app`
3. 如提示不安全：右键 → 打开

#### Linux
```bash
chmod +x docker-registry-explorer-linux-amd64
./docker-registry-explorer-linux-amd64
```

---

## 📖 使用指南

### 镜像浏览

1. **连接Registry**
   - 输入目标地址：`192.168.1.100:5000` 或 `registry.example.com`
   - 如需认证：填写用户名和密码
   - 点击"连接"按钮

2. **浏览和下载**
   - 勾选仓库 → 点击"批量下载" → 下载该仓库的所有标签
   - 选择仓库 → 查看标签 → 勾选标签 → 批量下载
   - 选择标签 → 查看层 → 勾选层 → 批量下载

3. **查看下载记录**
   - 切换到"下载历史记录"
   - 查看所有下载的文件
   - 可删除记录（文件同步删除）

### 认证爆破

1. **配置爆破**
   - 输入目标地址
   - 选择用户名字典文件
   - 选择密码字典文件
   - 设置线程数（1-100）
   - 设置延迟（毫秒）

2. **开始爆破**
   - 点击"开始爆破"
   - 观察实时日志
   - 找到凭证后自动停止

3. **使用凭证**
   - 爆破成功后弹窗询问是否跳转
   - 凭证自动填充到镜像浏览区域
   - 点击连接即可使用

### 敏感信息搜索

1. **选择搜索路径**
   - 默认选择download目录
   - 或点击"选择文件夹"自定义

2. **配置选项**（可选）
   - 自定义正则表达式
   - 自定义文件扩展名
   - 选择文件大小限制
   - 启用"自动解压压缩包"
   - 启用"仅使用自定义规则"

3. **开始搜索**
   - 点击"开始搜索"
   - 查看实时进度和结果
   - 结果自动保存到：`{时间戳}_info.txt`

4. **查看结果**
   - 实时显示在右侧结果区域
   - 点击"导出结果"打开文件所在目录

---

## ⚠️ 免责声明

**本工具仅供安全测试和授权渗透测试使用！**

- ✅ 仅在您拥有合法权限的环境中使用
- ✅ 用于自己管理的系统测试
- ✅ 安全研究和学习

**禁止行为**：
- ❌ 未经授权扫描他人系统
- ❌ 恶意爆破或窃取信息
- ❌ 用于非法目的

**违法使用后果自负！**

---

## 📞 获取支持

### 更新渠道

关注公众号：**棉花糖fans**
- 获取最新版本
- 功能更新通知
- 技术支持

### 版本检测

程序内置自动版本检测功能：
- 启动时自动检查（静默）
- 手动检查：系统配置管理 → 关于 → 检查更新

---

## 🙏 致谢

- [Wails](https://wails.io) - 优秀的Go跨平台桌面应用框架

---

## 📄 开源协议

MIT License

---

**Version**: 1.0.0  
**Author**: 棉花糖  
**Public Account**: 棉花糖fans

