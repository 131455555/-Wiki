# U-Boot 网络调试

## 这个概念是什么

U-Boot 网络调试是在 [[u-boot|U-Boot]] 阶段通过网络命令测试连通性、获取地址，或从主机下载启动镜像到开发板 DRAM 的调试方法。常见命令包括 `ping`、`dhcp`、`nfs` 和 `tftpboot`。

在 RK3568 驱动学习和内核调试中，网络调试常用于把 `boot.img`、内核、设备树或其他测试文件从 Ubuntu 主机下载到开发板内存，再直接启动或验证。

## 为什么重要

网络调试能显著缩短调试循环。相比反复烧写 eMMC 或 SD 卡，通过 TFTP / NFS 下载文件到 DRAM 更适合频繁验证内核和设备树改动。

它也帮助确认板卡早期网络能力是否正常：IP、网关、子网掩码、服务器地址、MAC 地址等配置都可以在 U-Boot 阶段暴露出来。

## 常用命令和变量

常见命令：

```bash
ping
dhcp
nfs
tftpboot
```

常见环境变量：

```bash
setenv ipaddr 192.168.5.4
setenv gatewayip 192.168.5.1
setenv netmask 255.255.255.0
setenv serverip 192.168.5.2
saveenv
```

变量含义：

- `ipaddr`：开发板 IP。
- `serverip`：服务器 IP，通常是 Ubuntu 主机。
- `gatewayip`：网关。
- `netmask`：子网掩码。
- `ethaddr`：MAC 地址，部分 U-Boot 默认禁止修改。

## 适用场景

- 使用 `ping` 验证开发板到主机的网络连通性。
- 使用 `dhcp` 自动获取 IP。
- 使用 `nfs` 从主机完整路径下载文件到 DRAM。
- 使用 `tftpboot` 或 `tftp` 从 TFTP 根目录下载文件。
- 下载 `boot.img` 后配合 [[boot-fit|boot_fit]] 启动。

## 注意点

U-Boot 可以主动 `ping` 其他机器，但其他机器通常不能反向 `ping` U-Boot，因为 U-Boot 一般不会像完整操作系统那样持续处理外部 ping 请求。

## 与其他概念的关系

- 网络参数通过 [[u-boot-environment-variables|U-Boot 环境变量]] 配置。
- 下载后的 RK3568 `boot.img` 可以通过 [[boot-fit|boot_fit]] 启动。
- 网络调试发生在 [[bootloader|Bootloader]] 阶段，是 [[u-boot|U-Boot]] 的重要调试能力。

## 相关来源

- [[rk3568-uboot-usage|RK3568 Linux驱动学习：U-Boot 使用]]

## 相关页面

- [[u-boot|U-Boot]]
- [[u-boot-environment-variables|U-Boot 环境变量]]
- [[boot-fit|boot_fit]]
- [[bootloader|Bootloader]]

