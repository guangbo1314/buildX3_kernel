# buildX3_kernel

[中文](README.zh-CN.md)

Kernel source for X3 (sharkl5pro / UMS512), Linux 4.14.193, Android 14 —
with KernelSU integrated (`kernel_x3/KernelSU/`).

Kernel is GPLv2; vendor-derived code and blobs remain property of their owners.

## Credits

Based on [rtyutechstudio/android_kernel_EEBBK_P21H180](https://github.com/rtyutechstudio/android_kernel_EEBBK_P21H180)
(unofficial EEBBK A3 / UMS512 kernel source).
Kernel: GPL-2.0 (see `kernel_x3/COPYING`); upstream additions: Apache-2.0 (see `kernel_x3/LICENSE`).

## Modifications (relative to upstream)

- KernelSU integration (`drivers/kernelsu/`, hooks in `sys/reboot/exec/input/kallsyms.c`, Kconfig/Makefile)
- SUSFS patches in `fs/` (guarded by `CONFIG_KSU_SUSFS*`; disabled in the shipped config)
- `i2c-sprd.c`: 750 ms transfer timeout guard
- mali Kbuild build adaptation (`platform/sharkl5Pro/Kbuild`)
- `sprd_sensor_core.c` / `sprd_sensor_drv.c`: experimental sensor changes (weak symbol, skip regulator power-on)
- `focaltech_esdcheck.c`: extra ESD status value `0x82`

## Build

```sh
export PATH=<clang-r383902b>/bin:$PATH
cd kernel_x3
make O=out ARCH=arm64 CC=clang CLANG_TRIPLE=aarch64-linux-gnu- \
     CROSS_COMPILE=<aarch64-linux-android-4.9>/bin/aarch64-linux-android- bootimage
```

Build trees (`kernel_x3/out*`) are not tracked.
