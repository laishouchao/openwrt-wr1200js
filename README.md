# OpenWrt Custom Firmware for YouHua WR1200JS

基于 OpenWrt 24.10.7 官方 ImageBuilder 定制的 WR1200JS 专用固件，通过 GitHub Actions 自动构建。

## 设备信息

| 项目 | 参数 |
|------|------|
| 型号 | YouHua WR1200JS |
| SoC | MediaTek MT7621AT (MIPS 1004Kc, 4核 880MHz) |
| RAM | 128MB DDR3 |
| Flash | 16MB SPI NOR (GD25Q128) |
| WiFi 2.4G | MediaTek MT7603E (b/g/n, 20dBm) |
| WiFi 5G | MediaTek MT76x2E (a/n/ac, 23dBm) |
| 网口 | 5x 千兆 (4 LAN + 1 WAN) |
| USB | 1x USB 3.0 |
| Target | ramips/mt7621 (mipsel_24kc) |

## 预装软件

### 系统管理
- **LuCI** — Web 管理界面 + **Argon 主题** + 中文语言包
- **nano** / **htop** / **curl** / **wget** — 常用工具

### 网络
- **wpad-openssl** — 完整 WiFi 功能 (AP/STA/WDS/Mesh/WPA3)
- **PPPoE** — 宽带拨号
- **SQM** — QoS 流控 (抗缓冲膨胀)
- **miniupnpd** — UPnP 端口映射

### DNS
- **SmartDNS** — 智能 DNS 解析

### VPN
- **WireGuard** — 高性能 VPN

### USB
- **USB 挂载** — ext4/vfat/exfat 自动挂载

### 其他
- **DDNS** — 动态域名
- **Wake-on-LAN** — 远程唤醒
- **HD Idle** — 硬盘休眠

> **注意**: 由于 16MB Flash 空间限制，v1.0.16 移除了 Samba4、OpenVPN、Adblock、relayd 以确保固件能正常刷入。如需这些功能，可通过 `opkg install` 在线安装。

## 固件信息

| 项目 | 值 |
|------|------|
| 版本 | v1.0.16 |
| OpenWrt | 24.10.7 r29197 |
| 内核 | 6.6.141 |
| 固件大小 | 10.94 MB |
| 已安装包 | 234 个 |

## 硬件支持

| 硬件 | 状态 |
|------|------|
| Power LED | ✅ |
| 2.4G WiFi LED | ✅ |
| 5G WiFi LED | ✅ |
| WPS LED | ✅ |
| Internet LED | ✅ |
| LAN 1-4 LED | ✅ (交换机硬件控制) |
| USB LED | ✅ |
| Reset 按钮 | ✅ (长按恢复出厂) |
| WPS 按钮 | ✅ |
| WiFi 按钮 | ✅ (开关无线) |
| 5x 千兆网口 | ✅ |
| 双频 WiFi | ✅ |
| USB 3.0 | ✅ |
| 串口 | ✅ (115200/8N1) |

## 下载

前往 [Releases](../../releases) 页面下载最新固件。

| 文件 | 用途 |
|------|------|
| `*-sysupgrade.bin` | 系统升级 / Breed 刷入 |

## 安装方法

### 方法一：Breed Web 恢复控制台（推荐）

适用于已刷入 Breed 的路由器。

1. 拔掉电源 → 按住 Reset 键不放 → 插上电源 → 等待 10 秒后松开
2. 电脑用网线连接 LAN 口，设置 IP `192.168.1.100`
3. 浏览器访问 `http://192.168.1.1`
4. 选择 **固件更新 → 固件**
5. 上传 `*-sysupgrade.bin` → 更新
6. 等待 2-3 分钟，路由器自动重启

### 方法二：SSH 命令行升级

适用于已运行 OpenWrt 的路由器。

```bash
# 1. 下载固件到路由器
scp openwrt-*-sysupgrade.bin root@192.168.1.1:/tmp/

# 2. SSH 登录路由器
ssh root@192.168.1.1

# 3. 执行升级（不保留配置）
sysupgrade -n /tmp/openwrt-*-sysupgrade.bin
```

### 方法三：LuCI Web 界面升级

适用于已运行 OpenWrt 的路由器。

1. 登录 `http://192.168.1.1`
2. 系统 → 备份/升级
3. 上传 `*-sysupgrade.bin`
4. 取消勾选"保留配置"（首次建议全新安装）
5. 执行升级

### 救砖：TFTP 刷入

如果固件刷入失败，可通过 TFTP 恢复。

1. 网线连接 LAN 口
2. 电脑设置 IP `192.168.1.100`
3. 按住 Reset 按钮通电，等待 10 秒松开
4. 通过 TFTP 上传 factory.bin

## 自定义构建

Fork 本仓库后，可通过 GitHub Actions 自动构建：

1. 修改 `.github/workflows/build.yml` 中的 `PACKAGES` 变量
2. Push 代码或创建 tag 触发构建
3. 在 Actions 页面下载构建产物

### 构建技术细节

- 使用 OpenWrt 官方 ImageBuilder 而非全量编译
- **Argon 主题**: 通过 `FILES` 机制直接注入根文件系统（从 dl.openwrt.ai 下载 .ipk 解压）
- **Flash 限制**: 固件大小控制在 16MB 以内
- **软件包策略**: 精选常用包，移除大体积包 (Samba4/OpenVPN/Adblock) 以适配空间

## 许可证

OpenWrt 使用 GPL-2.0 许可证。
