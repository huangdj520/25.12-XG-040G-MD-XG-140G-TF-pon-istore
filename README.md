# OpenWRT-CI

贝尔 040G 系列光猫 OpenWrt/PonWrt 固件云编译仓库。

---

## ✨ 本固件特征（AIR-ONU 编译流）

基于 **pbs05/ponwrt**（PON 专用源码）master 分支，内核 **6.18.55**，为贝尔 **XG-040G-MD（U-Boot + UBI 分区）** 光猫定制，输出 **ITB（.itb）** 镜像。设备名：**daepon**，登录地址 **192.168.1.1**（默认无密码），版本标识带 `build by zk6685`。

### 📡 光口 PON 全套
- kmod-airoha-xpon / kmod-airoha-pon-frontend（PON 底层驱动）
- airoha-ponctl / airoha-pond / airoha-pon-debug（PON 用户态工具）
- luci-app-pon（光口管理界面）

### 🛍️ iStoreX 首页 + iStore 商店
- luci-app-istorex（iStoreX 首页 / 应用管理面板）
- luci-app-quickstart + quickstart（新手引导首页）
- luci-app-store（iStore 应用商店本体）+ luci-lib-taskd / taskd / luci-lib-xterm

### 🛡️ dae / daed（eBPF 代理）全依赖 + BTF/CO-RE
内核已开启完整调试信息与 BTF（`DEBUG_INFO=y`、`DEBUG_INFO_BTF=y`、`DEBUG_INFO_REDUCED=n`、CGROUPS/CGROUP_BPF/BPF_EVENTS/BPF_TOOLCHAIN_HOST/XDP_SOCKETS），并内置全部内核依赖：
- kmod-sched-bpf / kmod-sched-core / kmod-veth / kmod-xdp-sockets-diag / kmod-nft-tproxy / ca-bundle

> dae / daed 二进制由用户自行安装（`opkg install dae daed`），本固件已备好 BTF 环境，可直接使用。

### 📊 Airoha SoC 状态面板
- luci-app-airoha-npu（**luanmuc 中文版**，NPU / CPU / Frame Engine 状态）+ 中文语言包（luci-i18n-airoha-npu-zh-cn）

### 🎨 其他内置
- luci-theme-aurora + luci-app-aurora-config（Aurora 主题）
- vlmcsd + luci-app-vlmcsd（KMS 激活服务）
- zram-swap + kmod-zram（内存压缩交换）
- luci-app-appfilter / luci-app-filemanager / luci-app-samba4 / luci-app-wolplus / luci-app-ddns

---

## ⚠️ 刷机前须知

刷机前必须备份所有原厂分区，特别是 **ri** 和 **bosa** 分区。

详细说明：
https://www.right.com.cn/forum/thread-8453612-1-1.html

### 支持设备

四个固件通用，设备名称只是区分不同功能。

**带 USB 设备**：
- XG-040G-MD　XG-140G-MD（lan4 wan）

**不带 USB 设备**：
- XG-040G-TF　XG-140G-TF（lan4 wan）

上游源码：
https://github.com/bingoguo93/immortalwrt.git

---

## 🔄 恢复 MAC 地址说明

刷机前必须备份所有原厂分区，特别是 ri 和 bosa 分区，参考详细说明刷回备份。

## 📅 编译说明

固件每天早上 5 点自动编译。

固件信息里的时间为编译开始的时间，方便核对上游源码提交时间。

覆盖贝尔 040 系列、140 系列。

## 📁 目录简要说明

- `.github/workflows` —— 自定义 CI 配置（AIR-ONU / AIR-NWRT / AIR-MAIN 等编译流）
- `Scripts` —— 自定义脚本（软件包拉取、设置项注入）
- `Config` —— 自定义配置（AIROHA-ONU 等目标配置）
