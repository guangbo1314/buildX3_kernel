# buildX3_kernel

[English](README.md)

X3（sharkl5pro / UMS512）内核源码工程，Linux 4.14.193，Android 14——
已集成 KernelSU（`kernel_x3/KernelSU/`）。

内核本体为 GPLv2；厂商衍生代码与 blob 版权仍归其所有者。

## 来源声明（Credits）

本仓库基于 [rtyutechstudio/android_kernel_EEBBK_P21H180](https://github.com/rtyutechstudio/android_kernel_EEBBK_P21H180)
（EEBBK A3 / UMS512 非官方内核源码）修改而来。

- 内核本体：**GPL-2.0**（见 `kernel_x3/COPYING`）
- 上游补充内容：**Apache-2.0**（见 `kernel_x3/LICENSE`）

## 相对上游的修改清单

- KernelSU 集成（`drivers/kernelsu/`，`sys/reboot/exec/input/kallsyms.c` 五处钩子，Kconfig/Makefile）
- SUSFS 补丁（`fs/` 下 18 个文件，由 `CONFIG_KSU_SUSFS*` 守卫——**发布配置中未启用**）
- `i2c-sprd.c`：传输 750ms 超时保护
- mali Kbuild 构建适配（`platform/sharkl5Pro/Kbuild`）
- `sprd_sensor_core.c` / `sprd_sensor_drv.c`：sensor 实验性修改（weak 符号、跳过 regulator 上电）
- `focaltech_esdcheck.c`：ESD 状态判断补充 `0x82`

## 构建方法

```sh
export PATH=<clang-r383902b>/bin:$PATH
cd kernel_x3
make O=out ARCH=arm64 CC=clang CLANG_TRIPLE=aarch64-linux-gnu- \
     CROSS_COMPILE=<aarch64-linux-android-4.9>/bin/aarch64-linux-android- bootimage
```

构建树（`kernel_x3/out*`）不纳入版本管理。
