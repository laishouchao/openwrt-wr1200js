# OpenWrt 24.10.7 for YouHua WR1200JS

自定义 OpenWrt 固件，基于官方 ImageBuilder 构建，专为友华 WR1200JS 路由器优化。

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
- **静态地址** — 固定 IP 配置（已内置在 LuCI 中）
- **LuCI + Argon 主题** — 现代化 Web 管理界面
- **中文界面** — 完整中文支持
- **WiFi 双频** — 2.4G + 5G 双频 AP
- **USB 扩展** — 支持 USB 存储挂载和 extroot 扩容

## 预装软件

| 分类 | 软件 |
|------|------|
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

1. 下载最新 Release 中的 `squashfs-sysupgrade.bin` 文件
2. 刷入 Breed 后断电，按住 WiFi 按钮插电，访问 `192.168.1.1` 进入 Breed
3. 恢复出厂后刷入之前下载的 bin 文件

## 更新日志

### v1.0.31
- 移除 frpc，精简固件体积
- 保留所有基础功能：WiFi、PPPoE、SmartDNS、SQM、DDNS、UPnP 等

## 硬件支持

- ✅ 所有 10 个 LED 灯 (Power/2.4G/5G/WPS/Internet/LAN1-4/USB)
- ✅ 所有 3 个按钮 (Reset/WPS/WiFi)
- ✅ 5 个千兆网口 (4 LAN + 1 WAN)
- ✅ 双频 WiFi (2.4G b/g/n + 5G a/n/ac)
- ✅ USB 3.0 端口
- ✅ 串口 (115200/8N1)

## 下载

[Releases](https://github.com/laishouchao/openwrt-wr1200js/releases)
