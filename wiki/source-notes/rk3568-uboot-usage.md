# RK3568 Linux驱动学习：U-Boot 使用

## 来源信息

- 原始文件：[[raw/2026-05-08-rk3568-uboot-usage.md|2026-05-08-rk3568-uboot-usage]]
- 原文链接：https://zhuanlan.zhihu.com/p/1932870593348366415
- 作者 / 来源：嵌入式新晋职工 / 知乎
- 日期：2026-05-08
- 主题：[[u-boot|U-Boot]]、[[bootloader|Bootloader]]、RK3568、Linux 驱动调试

## 核心观点

这篇资料围绕 RK3568 开发板上的 [[u-boot|U-Boot]] 使用展开。它把 U-Boot 放在 Linux 启动链路中理解：芯片上电后先运行 [[bootloader|Bootloader]]，完成 DDR 等基础外设初始化，再把 Linux 内核和设备树等启动材料从 Flash、SD 卡或 eMMC 等介质加载到 DRAM，最后跳转启动 Linux。

资料的价值不在于介绍 U-Boot 源码，而在于整理了开发板调试时会直接用到的命令：查询命令、[[u-boot-environment-variables|U-Boot 环境变量]]、内存操作、[[u-boot-network-debugging|U-Boot 网络调试]]、MMC / EXT4 文件系统访问，以及 RK3568 上较重要的 [[boot-fit|boot_fit]] 启动方式。

## 关键提炼

- [[u-boot|U-Boot]] 是 Linux 启动前运行的开源 bootloader，核心任务是把 Linux 内核启动起来。
- RK3568 开发中通常使用瑞芯微 SDK 或板卡厂商 SDK 中已经适配过的 U-Boot，而不是直接使用上游 U-Boot。
- 通过串口终端在自动启动倒计时阶段按下 `CTRL+C`，可以进入 U-Boot 命令行。
- `setenv` 修改的是内存中的环境变量，`saveenv` 才会把变量保存到外部 Flash 或 eMMC。
- U-Boot 支持 `ping`、`dhcp`、`nfs`、`tftpboot` 等网络命令，适合在内核、设备树和镜像调试时快速下载文件到 DRAM。
- RK3568 常见启动文件是 `boot.img`，其中打包了 Linux 内核 Image 和设备树，因此常用 [[boot-fit|boot_fit]]，而不是传统的 `bootm` 或 `bootz`。
- `boot` 和 `bootd` 会执行环境变量 `bootcmd`；在 RK3568 场景中，`bootcmd` 默认通常会调用 `boot_fit`。

## 可沉淀的知识页

- [[u-boot|U-Boot]]
- [[bootloader|Bootloader]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[u-boot-network-debugging|U-Boot 网络调试]]
- [[boot-fit|boot_fit]]

## 待继续追问

- RK3568 的 `boot.img` 内部具体包含哪些结构和镜像？
- `boot_fit` 如何解析并选择 `boot.img` 中的内核、设备树和配置？
- U-Boot 环境变量在不同板卡上具体保存到 eMMC 的哪个区域？
- RK3568 的 eMMC 分区布局如何影响启动、升级和恢复？
- TFTP 启动、NFS 下载和 eMMC 启动在驱动调试工作流中的取舍是什么？

## 相关页面

- [[u-boot|U-Boot]]
- [[bootloader|Bootloader]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[u-boot-network-debugging|U-Boot 网络调试]]
- [[boot-fit|boot_fit]]

