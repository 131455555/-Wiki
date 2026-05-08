# U-Boot 环境变量

## 这个概念是什么

U-Boot 环境变量是 U-Boot 运行时保存启动配置和调试配置的一组键值对。常见变量包括 `bootcmd`、`bootdelay`、`ipaddr`、`serverip`、`gatewayip`、`netmask` 和 `ethaddr`。

环境变量可以通过 `printenv` 查看，通过 `setenv` 修改，通过 `saveenv` 持久化保存。需要注意的是，`setenv` 修改的是当前 DRAM 中的环境变量；如果不执行 `saveenv`，重启后修改通常不会保留。

## 为什么重要

环境变量直接影响 [[u-boot|U-Boot]] 如何启动系统。比如：

- `bootdelay` 决定自动启动前等待多长时间。
- `bootcmd` 决定倒计时结束后执行什么启动命令。
- `ipaddr`、`serverip`、`gatewayip` 和 `netmask` 决定 [[u-boot-network-debugging|U-Boot 网络调试]] 能否正常工作。

理解环境变量，是从“会敲命令”走向“能控制启动流程”的关键一步。

## 常用命令

```bash
printenv
setenv
saveenv
```

示例：修改启动倒计时并保存。

```bash
setenv bootdelay 3
saveenv
```

示例：新增变量。

```bash
setenv author 'alientek'
saveenv
```

示例：删除变量。

```bash
setenv author
saveenv
```

## 适用场景

- 调整自动启动等待时间，方便进入 U-Boot 命令行。
- 修改默认启动命令，例如让 `bootcmd` 调用 [[boot-fit|boot_fit]]。
- 设置网络参数，配合 TFTP 或 NFS 下载 `boot.img`。
- 临时验证某种启动路径，然后再决定是否持久化保存。

## 与其他概念的关系

- 环境变量是 [[u-boot|U-Boot]] 的配置机制。
- `bootcmd` 可以调用 [[boot-fit|boot_fit]]，从而自动启动 RK3568 的 `boot.img`。
- 网络相关变量支撑 [[u-boot-network-debugging|U-Boot 网络调试]]。
- 环境变量的持久化位置可能依赖具体板卡和存储布局，常见保存介质包括外部 Flash 或 eMMC。

## 相关来源

- [[rk3568-uboot-usage|RK3568 Linux驱动学习：U-Boot 使用]]

## 相关页面

- [[u-boot|U-Boot]]
- [[bootloader|Bootloader]]
- [[u-boot-network-debugging|U-Boot 网络调试]]
- [[boot-fit|boot_fit]]

