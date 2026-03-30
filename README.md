# 🎮 Clash-Deck

**Steam Deck 全局 SOCKS5 代理插件**

基于 [Clash Meta (mihomo)](https://github.com/MetaCubeX/mihomo) 核心，为 Steam Deck 提供一键式全局代理解决方案。

---

## ✨ 功能特性

| 功能 | 说明 |
|------|------|
| 🌐 全局代理 | SOCKS5 / HTTP / HTTPS 全协议支持 |
| 🎮 Steam 优化 | 内置 Steam 相关域名路由规则 |
| 🖥 GUI 界面 | 支持图形界面 (yad/zenity) 与 TUI 终端界面 |
| ⚙️ 规则路由 | 支持 GeoIP、域名、IP-CIDR 等灵活规则 |
| 🔄 自启动 | 支持 systemd 用户服务和 XDG autostart |
| 🌍 多协议 | SOCKS5 / Shadowsocks / VMess / Trojan |

---

## 📥 快速开始

### 方式一：直接下载 AppImage

```bash
# 下载（替换为实际发布地址）
wget https://github.com/your-repo/clash-deck/releases/latest/download/Clash-Deck-x86_64.AppImage

# 赋予执行权限
chmod +x Clash-Deck-x86_64.AppImage

# 运行安装
./Clash-Deck-x86_64.AppImage
```

### 方式二：从源码构建

```bash
git clone https://github.com/your-repo/clash-deck
cd clash-deck

# 构建 AppImage（需要联网下载 clash-core 和 appimagetool）
chmod +x build.sh
./build.sh
```

---

## ⚙️ 配置说明

配置文件位于 `~/.config/clash-deck/config.yaml`

### 配置 SOCKS5 代理服务器

```yaml
proxies:
  - name: "my-socks5"
    type: socks5
    server: YOUR_SERVER_IP   # ← 填写你的服务器 IP
    port: 1080               # ← 填写端口
    # username: user         # 如需认证取消注释
    # password: pass
```

### 配置 Shadowsocks

```yaml
proxies:
  - name: "my-ss"
    type: ss
    server: YOUR_SERVER_IP
    port: 8388
    cipher: aes-256-gcm
    password: YOUR_PASSWORD
```

### 配置 VMess (V2Ray)

```yaml
proxies:
  - name: "my-vmess"
    type: vmess
    server: YOUR_SERVER_IP
    port: 443
    uuid: YOUR_UUID
    alterId: 0
    cipher: auto
    tls: true
```

---

## 🖥 使用方式

```bash
# 启动图形界面
clash-deck

# 命令行操作
clash-deck start      # 启动代理
clash-deck stop       # 停止代理
clash-deck restart    # 重启代理
clash-deck status     # 查看状态
clash-deck config     # 编辑配置
clash-deck log        # 查看日志
```

---

## 🌐 代理端口

| 类型 | 地址 |
|------|------|
| HTTP 代理 | `http://127.0.0.1:7890` |
| SOCKS5 代理 | `socks5://127.0.0.1:7891` |
| 混合端口 | `http://127.0.0.1:7890` |
| API 面板 | `http://127.0.0.1:9090/ui` |

---

## 🎮 Steam Deck 特别说明

### 游戏模式使用

在游戏模式下，Steam 本身使用系统代理环境变量。
安装后代理变量会自动写入 `/etc/profile.d/clash-deck-proxy.sh`。

### 透明代理（需要 root）

Steam Deck 进入桌面模式后：

```bash
# 设置 sudo 密码（如果未设置）
passwd

# 以 root 运行以启用透明代理（无需手动设置每个应用）
sudo clash-deck start
```

### 测试代理连接

```bash
# 测试 SOCKS5
curl --socks5 127.0.0.1:7891 https://www.google.com -I

# 测试 HTTP
curl --proxy http://127.0.0.1:7890 https://www.google.com -I
```

---

## 📁 文件结构

```
~/.config/clash-deck/
├── config.yaml      # 主配置文件
├── logs/            # 日志目录
└── Country.mmdb     # GeoIP 数据库（自动下载）
```

---

## 🔧 故障排查

**代理不工作？**
1. 检查 `clash-deck status` 确认运行中
2. 确认配置文件中服务器地址正确
3. 查看日志 `clash-deck log`
4. 检查服务器是否可达：`ping YOUR_SERVER`

**Steam 游戏无法走代理？**
- 游戏模式需要重新登录后环境变量才生效
- 或使用透明代理模式（需 root）

**AppImage 无法运行？**
```bash
# Steam Deck 可能需要 FUSE
sudo pacman -S fuse2
# 或直接挂载运行
./Clash-Deck-x86_64.AppImage --appimage-extract
./squashfs-root/AppRun
```

---

## 📄 许可证

MIT License - 基于 [Clash Meta](https://github.com/MetaCubeX/mihomo) 开源项目

---

*专为 Steam Deck 优化 | Powered by Clash Meta*
