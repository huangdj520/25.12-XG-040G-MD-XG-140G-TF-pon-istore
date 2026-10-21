# OpenWRT-CI

**贝尔 040 系列光猫 OpenWrt / PonWrt 固件云编译仓库**

> 固件免费开源分享。如果它帮你省了事、省了心，欢迎扫码支持一下 ☕ —— 你的每一份心意，都是我继续编译、持续更新的动力。
>
> <img src="docs/donate.png" alt="赞赏码" width="240"/>

---

## ✨ 本固件特征（AIR-ONU 编译流）

基于 **pbs05/ponwrt**（PON 专用源码）master 分支，内核 **6.18.55**，面向 **airoha / an7581 平台** 全系光猫定制，输出 **ITB（.itb）** 镜像。固件统一以 **`zk-daepon-`** 为文件名前缀；设备名 **daepon**，登录地址 **192.168.1.1**（默认无密码），版本标识带 `build by zk6685`。

### 📡 光口 PON 全套
- kmod-airoha-xpon / kmod-airoha-pon-frontend（PON 底层驱动）
- airoha-ponctl / airoha-pond / airoha-pon-debug（PON 用户态工具）
- luci-app-pon（光口管理界面）

### 🛍️ iStoreX 首页 + iStore 商店
- luci-app-istorex（iStoreX 首页 / 应用管理面板）
- luci-app-quickstart + quickstart（新手引导首页）
- luci-app-store（iStore 应用商店本体）+ luci-lib-taskd / taskd / luci-lib-xterm

### 🛡️ dae / daed（eBPF 代理）全依赖 + BTF / CO-RE
内核已开启完整调试信息与 BTF（`DEBUG_INFO=y`、`DEBUG_INFO_BTF=y`、`DEBUG_INFO_REDUCED=n`、CGROUPS / CGROUP_BPF / BPF_EVENTS / BPF_TOOLCHAIN_HOST / XDP_SOCKETS），并内置全部内核依赖：
- kmod-sched-bpf / kmod-sched-core / kmod-veth / kmod-xdp-sockets-diag / kmod-nft-tproxy / ca-bundle

> dae / daed 二进制由用户自行安装（`opkg install dae daed`），本固件已备好 BTF 环境，可直接使用。

### 📊 Airoha SoC 状态面板
- luci-app-airoha-npu（**luanmuc 中文版**，NPU / CPU / Frame Engine 状态）+ 中文语言包（luci-i18n-airoha-npu-zh-cn）

### 🎨 其他内置
- luci-theme-aurora + luci-app-aurora-config（Aurora 主题）
- vlmcsd + luci-app-vlmcsd（KMS 激活服务）
- zram-swap + kmod-zram（内存压缩交换）
- luci-app-appfilter / luci-app-filemanager / luci-app-samba4 / luci-app-wolplus / luci-app-ddns

### 📦 支持机型（同平台全系一次编译产出）
| 品牌 | 机型 | 变体 |
|---|---|---|
| **Nokia** | XG-040G-MD | ubi / ubi-usb-sfp |
| **Nokia** | XG-040G-TF | ubi |
| **烽火** FiberHome | HG5382A | — |
| **烽火** FiberHome | HG5585F | ct / cu |
| **Gemtek** | XG2010G | — |
| **Unionman** | UNG00A | — |
| **中兴 ZNXT** | ZN504XG-D / ZN515XG-D | — |

### 🏷️ 固件命名规则
```
zk-daepon-<平台设备>-squashfs-sysupgrade-<源码>-<分支>-<日期>.itb
```
例：`zk-daepon-airoha-an7581-nokia_xg-040g-md-ubi-squashfs-sysupgrade-pbs05-master-26.10.22-XX.XX.XX.itb`

> ⚠️ 各机型固件虽共用同一内核 / 插件 / PON 配置，但**内存颗粒、分区布局、外设可能不同，切勿混刷**，请按设备名选择对应 `.itb`。

---

## ⚠️ 刷机前须知

刷机前**必须备份所有原厂分区，特别是 `ri` 和 `bosa` 分区**。详细说明见恩山论坛：

https://www.right.com.cn/forum/thread-8453612-1-1.html

### 支持设备（传统分区版）

四个固件通用，设备名称仅用于区分不同功能。

**带 USB 设备**：XG-040G-MD　XG-140G-MD（lan4 wan）
**不带 USB 设备**：XG-040G-TF　XG-140G-TF（lan4 wan）

上游源码：https://github.com/bingoguo93/immortalwrt.git

---

## 🔄 恢复 MAC 地址

刷机前同样需先备份原厂分区（尤其 `ri` / `bosa`），刷机后如需恢复 MAC 地址，按详细说明刷回备份即可。

## 📅 编译说明

- 固件**每天早上 5 点自动编译**。
- 固件信息里的时间为编译开始的时间，方便核对上游源码提交时间。
- 覆盖贝尔 040 系列、140 系列。

## 📁 目录简要说明

- `.github/workflows` —— 自定义 CI 配置（AIR-ONU / AIR-NWRT / AIR-MAIN 等编译流）
- `Scripts` —— 自定义脚本（软件包拉取、设置项注入）
- `Config` —— 自定义配置（AIROHA-ONU 等目标配置）

---

## ☕ 赞赏支持

固件为**免费开源**分享。如果你觉得好用，欢迎扫码支持一杯咖啡，让我有动力持续维护、继续编译更新。

<img src="docs/donate.png" alt="赞赏码" width="240"/>
