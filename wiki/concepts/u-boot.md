# U-Boot

## 这个概念是什么

U-Boot，全称 Universal Boot Loader，是嵌入式 Linux 系统中常见的开源 [[bootloader|Bootloader]]。它运行在 Linux 内核之前，负责完成早期硬件初始化、准备启动参数、加载内核和设备树，并最终把控制权交给 Linux 内核。

在 RK3568 开发板场景中，U-Boot 通常来自瑞芯微 SDK 或板卡厂商 SDK 的适配版本，而不是直接使用上游 U-Boot。板卡厂商会在芯片厂商适配基础上继续加入开发板相关的 DDR、PMIC、存储介质、显示和默认启动命令配置。

## 为什么重要

U-Boot 是理解嵌入式 Linux 启动链路的入口。驱动开发、内核调试、设备树调试、系统烧写和启动失败排查，往往都需要先知道 U-Boot 在做什么。

它尤其重要的原因是：

- 它连接了硬件上电和 Linux 内核运行两个阶段。
- 它决定内核、设备树和根文件系统从哪里加载。
- 它通过 [[u-boot-environment-variables|U-Boot 环境变量]] 暴露启动策略，例如 `bootcmd`、`bootdelay`、`ipaddr` 和 `serverip`。
- 它提供 [[u-boot-network-debugging|U-Boot 网络调试]] 能力，可以通过 TFTP 或 NFS 把文件下载到 DRAM。

## 适用场景

- 通过串口进入 U-Boot 命令行，观察启动日志和板级信息。
- 查看当前 U-Boot 支持哪些命令，例如 `help`、`?`、`bdinfo`、`version`。
- 修改启动倒计时、启动命令、网络地址等环境变量。
- 从 eMMC、SD 卡、TFTP 或 NFS 加载启动镜像。
- 在 RK3568 上使用 [[boot-fit|boot_fit]] 启动 `boot.img`。

## 与其他概念的关系

- U-Boot 是 [[bootloader|Bootloader]] 的一种具体实现。
- [[u-boot-environment-variables|U-Boot 环境变量]] 决定 U-Boot 的启动行为和网络配置。
- [[u-boot-network-debugging|U-Boot 网络调试]] 依赖 U-Boot 的网络命令和网络环境变量。
- [[boot-fit|boot_fit]] 是 RK3568 场景中常用的 U-Boot 启动命令，用于启动打包后的 `boot.img`。

## 相关来源

- [[rk3568-uboot-usage|RK3568 Linux驱动学习：U-Boot 使用]]

## 相关页面

- [[bootloader|Bootloader]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[u-boot-network-debugging|U-Boot 网络调试]]
- [[boot-fit|boot_fit]]

