# Bootloader

## 这个概念是什么

Bootloader 是系统上电后、操作系统内核运行前执行的一段启动程序。它的主要职责是完成早期硬件初始化，把操作系统内核和必要启动材料加载到内存中，并把控制权交给内核。

在嵌入式 Linux 系统中，[[u-boot|U-Boot]] 是最常见的 bootloader 之一。以 RK3568 为例，芯片上电后会先进入 bootloader 阶段，初始化 DDR 等基础硬件，然后从 Flash、SD 卡或 eMMC 等存储介质读取 Linux 内核与设备树，最后启动 Linux。

## 为什么重要

Bootloader 决定了系统能否从硬件上电顺利走到内核运行。启动失败、内核无法加载、设备树不匹配、存储介质读取异常、启动参数错误等问题，很多都需要回到 bootloader 阶段分析。

对驱动开发来说，bootloader 还提供了一个快速调试入口：可以通过串口命令查看板级信息、读取存储、下载镜像、修改启动参数，而不必每次完整进入 Linux 系统后再排查。

## 适用场景

- 板卡上电启动流程分析。
- Linux 内核、设备树、根文件系统加载路径确认。
- 通过串口截停自动启动，进入启动命令行。
- 排查系统不能启动或启动到错误镜像的问题。
- 通过网络或存储介质临时加载测试镜像。

## 与其他概念的关系

- [[u-boot|U-Boot]] 是 bootloader 的一个具体实现。
- [[u-boot-environment-variables|U-Boot 环境变量]] 是 U-Boot 这类 bootloader 的可配置启动状态。
- [[boot-fit|boot_fit]] 是 U-Boot 在 RK3568 上引导 `boot.img` 的启动命令。
- [[u-boot-network-debugging|U-Boot 网络调试]] 是 bootloader 阶段常见的调试方式。

## 相关来源

- [[rk3568-uboot-usage|RK3568 Linux驱动学习：U-Boot 使用]]

## 相关页面

- [[u-boot|U-Boot]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[u-boot-network-debugging|U-Boot 网络调试]]
- [[boot-fit|boot_fit]]

