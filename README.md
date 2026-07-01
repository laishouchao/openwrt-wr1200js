# OpenWrt 24.10.7 for YouHua WR1200JS

自定义 OpenWrt 固件，基于官方 ImageBuilder 构建，专为优华 WR1200JS 路由器优化。

## 设备信息

| 项目 | 参数 |
|------|------|
| 型号 | YouHua WR1200JS |
| SoC | MediaTek MT7621AT (MIPS 1004Kc, 4核 880MHz) |
| RAM | 128MB |
| Flash | 16MB SPI NOR |
| WiFi | MT7603E (2.4G) + MT76x2E (5G) |
| Target | ramips/mt7621 (mipsel_24kc) |

## 固件特性

- **精简稳定** — 仅保留必要组件，适配 16MB flash 限制
- **frpc 0.69.1** — 内置最新版远程穿透客户端，支持 TOML 配置
- **luci-app-frpc-new** — 适配 TOML 格式的 LuCI Web 管理界面
- **静态地址** — 固定 IP 配置（已内置在 LuCI 中）
- **LuCI + Argon 主题** — 现代化 Web 管理界面
- **中文界面** — 完整中文支持
- **WiFi 双频** — 2.4G + 5G 双频 AP
- **USB 扩展** — 支持 USB 存储挂载和 extroot 扩容

## 预装软件

| 分类 | 软件 |
|------|------|
| 远程穿透 | frpc 0.69.1 + LuCI 管理界面 (SOCKS5/TCP/UDP) |
| Web 管理 | LuCI + Argon 主题 + 中文 |
| WiFi | wpad-openssl (AP/STA/WDS/Mesh/WPA3) |
| 拨号 | PPPoE |
| 网络 | 静态地址 / DHCP / DHCPv6 |
| DNS | SmartDNS |
| QoS | SQM (抗缓冲膨胀) |
| DDNS | 动态 DNS |
| UPnP | miniupnpd |
| 工具 | nano, htop, curl, wget, wol, hd-idle |
| USB | 存储挂载 (ext4/vfat/exfat) |

## 安装方法

- **首次刷入**: 使用 `*-factory.bin` 通过 Web 或 TFTP 刷入
- **升级更新**: 使用 `*-sysupgrade.bin` 通过 LuCI 或 `sysupgrade` 命令升级

## frpc 使用说明

frpc 已内置在固件中，支持两种配置方式：

### 方式一：LuCI Web 界面（推荐）
1. 登录 LuCI 管理界面 (http://192.168.2.1)
2. 进入 **服务 → frpc** 菜单
3. 填写服务器地址、端口、认证令牌
4. 添加代理规则（SOCKS5/TCP/UDP 等）
5. 保存后自动生效

### 方式二：命令行
```bash
# 编辑 UCI 配置
uci set frpc.main.server_addr='your-server.com'
uci set frpc.main.token='your-token'
uci commit frpc

# 启动 frpc
/etc/init.d/frpc start

# 设置开机自启
/etc/init.d/frpc enable
```

## 更新日志

### v1.0.30
- 新增 luci-app-frpc-new：适配 frpc 0.69.1 TOML 格式的 LuCI Web 管理界面
- 支持通过 Web 界面配置服务器连接、添加/编辑/删除代理规则
- 实时显示 frpc 运行状态、版本号、PID
- 自动将 UCI 配置转换为 TOML 格式（无需手动编辑 TOML 文件）
- 支持 TCP/UDP/HTTP/HTTPS/STCP/XTCP 代理类型
- 完整中文翻译

### v1.0.29
- 移除 iStore 应用商店和 xray-core（精简固件体积）
- 内置 frpc 0.69.1（最新版，支持 TOML 配置格式）
- 内置 frpc 启动脚本和示例配置
- 保留所有基础功能：WiFi、PPPoE、SmartDNS、SQM、DDNS、UPnP 等

### v1.0.28
- 修复构建配置：移除不存在的 luci-proto-static 包
- 更新 README 文档

### v1.0.27
- 首个基于 OpenWrt 24.10.7 的正式版本
- 内置 Xray-core v26.6.22
- 预装 iStore 应用商店
- 预装 ZeroTier 网络穿透

### v1.0.16
- 早期版本

## 硬件支持

- ✅ 所有 10 个 LED 灯 (Power/2.4G/5G/WPS/Internet/LAN1-4/USB)
- ✅ 所有 3 个按钮 (Reset/WPS/WiFi)
- ✅ 5 个千兆网口 (4 LAN + 1 WAN)
- ✅ 双频 WiFi (2.4G b/g/n + 5G a/n/ac)
- ✅ USB 3.0 端口
- ✅ 串口 (115200/8N1)

## 下载

[Releases](https://github.com/laishouchao/openwrt-wr1200js/releases)
