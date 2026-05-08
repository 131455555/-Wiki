# boot_fit

## 这个概念是什么

`boot_fit` 是 RK3568 U-Boot 场景中常用的启动命令，用于启动打包后的 `boot.img`。在该资料中，RK3568 的 `boot.img` 通常包含 Linux 内核 Image 和设备树文件，因此不能简单套用传统的 `bootm` 或 `bootz`，而是使用 `boot_fit`。

从默认 eMMC 启动时，可以直接执行：

```bash
boot_fit
```

从 TFTP 下载到 DRAM 后启动时，可以执行：

```bash
tftp E9EF7000 boot.img
boot_fit E9EF7000
```

## 为什么重要

`boot_fit` 是理解 RK3568 启动方式的关键入口。它解释了为什么同样是 U-Boot，引导 RK3568 的 `boot.img` 时可能不使用传统命令，而是使用和 FIT 镜像 / 打包镜像相关的启动路径。

在驱动调试中，`boot_fit` 还把 [[u-boot-network-debugging|U-Boot 网络调试]] 和实际启动动作连接起来：可以先用 TFTP 下载新的 `boot.img`，再用 `boot_fit` 从指定内存地址启动。

## 适用场景

- 从 eMMC 中按默认环境启动 RK3568 Linux。
- 从 TFTP 下载 `boot.img` 到 DRAM 后临时启动。
- 分析 `bootcmd` 自动启动流程。
- 对比 RK3568 启动方式与传统 `bootm` / `bootz` 的差异。

## 与其他概念的关系

- `boot_fit` 是 [[u-boot|U-Boot]] 中的启动命令。
- `boot` 和 `bootd` 会执行 [[u-boot-environment-variables|U-Boot 环境变量]] `bootcmd` 中定义的命令；RK3568 的 `bootcmd` 默认通常会调用 `boot_fit`。
- `boot_fit` 常和 [[u-boot-network-debugging|U-Boot 网络调试]] 结合，用于启动网络下载到 DRAM 的 `boot.img`。
- 它运行在 [[bootloader|Bootloader]] 阶段，最终目标是启动 Linux 内核。

## 相关来源

- [[rk3568-uboot-usage|RK3568 Linux驱动学习：U-Boot 使用]]

## 相关页面

- [[u-boot|U-Boot]]
- [[bootloader|Bootloader]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[u-boot-network-debugging|U-Boot 网络调试]]

